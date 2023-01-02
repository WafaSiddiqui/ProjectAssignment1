pipeline {
  environment {
    registry = "wafasidd/dockerfile1image"
    registryCredential = 'dockerHub'
    dockerImage = ''
  }
  agent any
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
           docker.image(registry + ":$BUILD_NUMBER").run('-d ')
        }
      }
    }
    if(currentBuild.result = 'FAILURE'){
      steps{
        docker container rm $(docker container ps -aq)
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
