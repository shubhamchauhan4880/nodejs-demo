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
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }                  
        stage('Pushing to ECR') {
            steps{  
                   script {
                           sh "docker tag nodeapp:$BUILD_NUMBER .790107037484.dkr.ecr.us-east-1.amazonaws.com/taskprac:latest"
                           sh "docker push 790107037484.dkr.ecr.us-east-1.amazonaws.com/taskprac:latest
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

