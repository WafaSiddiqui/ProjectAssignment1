#!groovy

pipeline {
	agent none  
 stages {
   stage('Cloning our Git') { 
          steps { 
              git 'https://github.com/WafaSiddiqui/ProjectAssignment1.git' 

            }

        }
    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker build -t wafasidd/dockerprojassignment1:latest .'
      }
    }
    stage('Docker Push') {
    	agent any
      steps {
      	withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push wafasidd/dockerprojassignment1:latest'
        }
      }
    }
  }
}
