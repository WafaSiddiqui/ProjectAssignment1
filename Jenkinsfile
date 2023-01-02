pipeline { 
    environment {
        registry = "wafasidd/dockerfile1image"
        registryCredential = 'dockerHub'
    }  
    agent any  
    stages {
        stage('Change Mode'){
            steps{
                sudo chmod 666 /var/run/docker.sock
            }
        }
        stage('Building image') {
            steps{
                script {
                    
                    sh 'docker build -t wafasidd/dockerfile1image:v2 .'
                }
            }
        }
        stage('Push Image to Docker Hub'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push wafasidd/dockerfile1image:v2'
                }
            }
        }
    }
}
