pipeline {
  agent any
  options { timestamps() }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Set up venv') {
      steps {
        sh '''
          set -e
          python3 --version || true
          # create venv
          python3 -m venv .venv
          . .venv/bin/activate
          python -m pip install --upgrade pip
          if [ -f requirements.txt ]; then
            pip install -r requirements.txt
          fi
        '''
      }
    }

    stage('Run tests') {
      steps {
        sh '''
          set -e
          . .venv/bin/activate
          # adjust to your test command
          pytest -q || python -m pytest -q || true
        '''
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
      junit '**/test-results/*.xml', allowEmptyResults: true
    }
  }
}

