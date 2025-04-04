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
        bat 'echo "building the app"'
      }
    }
    stage('Test'){
      steps{
        bat 'echo "Running tests"'
      }
    }
    stage('Deploy'){
      steps{
        bat 'echo "deploying"'
      }
    }
  }
}
