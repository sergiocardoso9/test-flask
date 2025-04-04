pipeline{
  agent any
  stages{
    stage('Checkout Code'){
      steps{
        git branch: 'main', url: 'https://github.com/Parth2k3/test-flask.git'

      }
    }
    stage('Build'){
      steps{
        sh 'echo "building the app"'
      }
    }
    stage('Test'){
      steps{
        sh 'echo "Running tests"'
      }
    }
    stage('Deploy'){
      steps{
        sh 'echo "deploying"'
      }
    }
  }
}
