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
           def container_runner = docker.image(registry + ":$BUILD_NUMBER").run('-d ')
        }
       
      
    
      }
    }
    when(stageResult:"FAILURE"){
      script{
        container_runner.stop()
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
