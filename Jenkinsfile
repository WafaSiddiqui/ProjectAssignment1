pipeline { 
    environment {
        registry = "wafasidd/dockerfile1image"
        registryCredential = 'dockerHub'
    }  
    agent any  
    stages {
        stage('Building image') {
            steps{
                script {
                    docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
    }
}
