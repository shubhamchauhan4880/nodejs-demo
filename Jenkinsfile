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
         stage('Deploy') {
            steps {
                script{
                        sh'aws configure'
                        sh'AWS Access Key ID [None]:AKIA3P5QMT4WCRHW7PNE '
                        sh'AWS Secret Access Key [None]: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'
                        sh'Default region name [None]: us-east-1'
                        sh'Default output format [None]: json'
                        sh 'docker tag shubhamchauhan4880/nodeapp:$BUILD_NUMBER 790107037484.dkr.ecr.us-east-1.amazonaws.com/taskprac:version1'
                        sh 'docker push 790107037484.dkr.ecr.us-east-1.amazonaws.com/taskprac:version1'
                       }
                    }
         }
}
         }
    }

