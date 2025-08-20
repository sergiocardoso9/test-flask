pipeline {
  agent any
  triggers { cron('* * * * *') }
  options { timestamps() }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('Set up venv') {
      steps {
        sh '''
          set -e
          python3 -V
          rm -rf .venv
          python3 -m venv .venv
          . .venv/bin/activate
          python -m pip install --upgrade pip
          [ -f requirements.txt ] && pip install -r requirements.txt
          pip install pytest
        '''
      }
    }
    stage('Run tests') {
      steps {
        sh '''
          set -e
          . .venv/bin/activate
          export PYTHONPATH=$PYTHONPATH:$(pwd)
          mkdir -p test-results
          pytest -q --junitxml=test-results/pytest.xml
        '''
      }
    }
  }
  post {
    always {
      archiveArtifacts artifacts: 'test-results/*.xml', allowEmptyArchive: true
      junit 'test-results/*.xml'
    }
  }
}
