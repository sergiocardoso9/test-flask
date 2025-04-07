pipeline{
  agent any
  environment{
    AWS_REGION = 'ap-south-1'
    IMAGE_NAME = 'test-flask'
    REPO_NAME = 'test'
    IMAGE_TAG = 'latest'
  }
  stages{
    stage('checkout'){
      steps{
        git branch:'main', url: 'https://github.com/Parth2k3/test-flask'
      }
    }   
    stage('Login to ECR'){
          steps{
            withAWS(region: "${env.AWS_REGION}", credentials: 'aws-creds'){
              powershell '''
              $password = aws ecr get-login-password --region ap-south-1
              docker login --username AWS --password $password 864981751441.dkr.ecr.ap-south-1.amazonaws.com
              '''
            }
          }
    }
    stage('Build Docker Image'){
          steps{
            powershell '''
            docker build -t ${env.IMAGE_NAME} .
            docker tag ${env.IMAGE_NAME}:${env.IMAGE_TAG} 864981751441.dkr.ecr.ap-south-1.amazonaws.com/test:latest
            '''
          }
    }
    stage('Push to ECR'){
      steps{
        powershell '''
        docker push 864981751441.dkr.ecr.ap-south-1.amazonaws.com/test:latest
        '''
      }
    }
  }
  
}
