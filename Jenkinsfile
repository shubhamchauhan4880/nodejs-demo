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
        stage('Pushing to ECR') {
                      steps{
                           script {
                                    sh'docker tag shubhamchauhan4880/nodeapp:1 790107037484.dkr.ecr.us-east-1.amazonaws.com/taskprac:version1'
                                    sh'docker push 790107037484.dkr.ecr.us-east-1.amazonaws.com/taskprac:version1'
                           }
                      } 
        }
        stage('Deployment'){
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'my-eks-cluster', contextName: '', credentialsId: 'mykubeconfig', namespace: '', serverUrl: 'https://351106EC9AD733FA5299F5B4269480ED.gr7.us-east-1.eks.amazonaws.com') {
                                                                                          
                                                        sh'kubectl apply -f Deployment.yml'
                                    

}
                        
           
}
                 
                      
                 }
        }
    
}

