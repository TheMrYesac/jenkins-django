pipeline{
  agent any
  environment{
    VENV = 'venv'
  }
  stages{
    stage('Checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/TheMrYesac/jenkins-django'
      }
    }
    stage('Login to ECR'){
      steps{
        withAWS(region: 'us-east-2', credentials: 'aws'){
          powershell '''
          $password = aws ecr get-login-password --region us-east-2
          docker login --username AWS --password $password 520320208152.dkr.ecr.us-east-2.amazonaws.com
          '''
        }
      }
    }
    stage('Build the docker image'){
      steps{
        powershell '''
        docker build -t jenkins-django:django .
        docker tag jenkins-django:django 520320208152.dkr.ecr.us-east-2.amazonaws.com/jenkins-django:django
        '''
      }
    }
    stage('Push image to ECR'){
      steps{
        powershell '''
        docker push 520320208152.dkr.ecr.us-east-2.amazonaws.com/jenkins-django:django
        '''
      }
    }
  }
}
