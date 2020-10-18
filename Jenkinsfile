pipeline {
  environment {
    registry = "adititanna/devsecopstraining"
    registryCredential = "DockerHub"
    dokerImage = ''
  }
  
  agent any
  
  stages {
    stage('Build Docker Image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    
    stage('Push to DockerHub') {
      steps {
        script {
          docker.withRegistry('', registryCredential) {
            docker.Image.push()
          }
        }  
      }
    }
    
    stage('Test Run') {
      steps {
        sh 'docker run -d $registry:$BUILD_NUMBER'
      }
    }
  }
}
