pipeline {
    agent any

    environment {
        VENV = 'venv'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/parth2k3/test-flask.git'
            }
        }

        stage('Set up Python Virtual Env') {
            steps {
                bat 'python -m venv %VENV%'
                bat '%VENV%\\Scripts\\python -m pip install --upgrade pip'
                bat '%VENV%\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat '%VENV%\\Scripts\\python -m unittest discover -s tests'
                // Optional: If using xmlrunner
                // bat '%VENV%\\Scripts\\python -m xmlrunner discover -s tests -o test-reports'
            }
        }
    }
        // Optional: only if generating XML test reports
        post {
             always {
                 junit 'test-reports/**/*.xml'
             }
         }
    
}
