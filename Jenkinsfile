pipeline{
  agent any
  environment{
    IMAGE_NAME = 'themryesac/jenkins-django'
  }
  stages{
    stage('Checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/TheMrYesac/jenkins-django'
      }
    }
    stage('Build the docker image'){
      steps{
        powershell '''
        docker build -t ${IMAGE_NAME}:latest .
        '''
      }
    }
    stage('Push to DockerHub'){
      steps{
        withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
        powershell '''
          echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
          docker push ${IMAGE_NAME}:latest
          docker logout
          '''
        }
      }
    }
  }
}
