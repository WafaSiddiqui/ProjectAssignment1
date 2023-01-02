pipeline {
  environment {
    registry = "wafasidd/dockerfile1image"
    registryCredential = 'dockerHub'
    dockerImage = ''
  }
  agent {label 'worker1'}
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/WafaSiddiqui/ProjectAssignment1.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Run') {
      steps{
        script{
           def container_runner = docker.image(registry + ":$BUILD_NUMBER").run('-d ')
        }
    
      }
    }
    
  
  }
  post { 
        unsuccessful { 
            echo 'Build failed!'
            script{
              container_runner.stop()
            }
        }
    }
}
