pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('Docker_hub_passs')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/ravdy/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t shubhamchauhan4880/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('Logging into AWS ECR') {
              steps {
                    script {
                               sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 790107037484.dkr.ecr.us-east-1.amazonaws.com'
                 }
              }
        }

}
}

