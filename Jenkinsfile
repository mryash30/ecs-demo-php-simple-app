
pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }

        stage('Build') {
            steps {
      	        sh 'docker build -t phpbuild:${BUILD_NUMBER} .'
            }
        }
        stage('Deploy') {
            steps {
                script{
                     docker.withRegistry('https://916123444654.dkr.ecr.us-east-1.amazonaws.com/phpdemo:latest', 'ecr:us-east-1:aws-credentials') {
                         sh 'docker tag phpdemo:latest 916123444654.dkr.ecr.us-east-1.amazonaws.com/phpdemo:${BUILD_NUMBER}'
                         sh 'docker push 916123444654.dkr.ecr.us-east-1.amazonaws.com/phpdemo:${BUILD_NUMBER}'  
                   }
                }
            }
        }
    }
}
