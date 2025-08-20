pipeline {
  agent any

  // Run this on a schedule. Examples:
  // 'H/5 * * * *'  -> every ~5 minutes (hashed spread)
  // 'H H * * *'    -> once daily at a hashed time
  // 'H/15 * * * *' -> every ~15 minutes
  triggers {
    cron('* * * * *')
  }

  options {
    timestamps()
    ansiColor('xterm')
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Set up Python venv') {
      steps {
        sh '''
          set -e
          python3 --version
          python3 -m venv .venv
          . .venv/bin/activate
          python -m pip install --upgrade pip
          # ensure pytest is present even if not in requirements.txt
          if [ -f requirements.txt ]; then
            pip install -r requirements.txt
          fi
          pip install pytest
        '''
      }
    }

    stage('Run tests') {
      steps {
        sh '''
          set -e
          . .venv/bin/activate
          # create folder for junit xml
          mkdir -p test-results
          # run tests; adjust pattern if your tests differ
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
