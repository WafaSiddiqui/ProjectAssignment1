#!groovy

pipeline {
	  
 stages {
   stage('Checkout') {
            git url: 'https://github.com/saurabh0010/sample-spring-microservices.git'
        }
    stage('Docker Build') {
    	
      steps {
      	sh 'docker build -t wafasidd/dockerprojassignment1:latest .'
      }
    }
    stage('Docker Push') {
    	
      steps {
      	withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push wafasidd/dockerprojassignment1:latest'
        }
      }
    }
  }
}
