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
    stage('Set Up VENV'){
      steps{
        bat 'python -m venv %VENV%'
        bat '%VENV%\\Scripts\\python -m pip install --upgrade pip'
        bat '%VENV%\\Scripts\\pup install -r requirements.txt'
      }
    }
    stage('Run tests'){
      steps{
        bat '%VENV%\\Scripts\\python manage.py test'
        }
      }
    }
  }
