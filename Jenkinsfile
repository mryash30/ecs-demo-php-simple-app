
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
      	        sh 'docker build -t phpbuild:latest .'
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{
                    sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 916123444654.dkr.ecr.us-east-1.amazonaws.com'
                    sh 'docker tag phpdemo:latest 916123444654.dkr.ecr.us-east-1.amazonaws.com/phpdemo:latest'
                    sh 'docker push 916123444654.dkr.ecr.us-east-1.amazonaws.com/phpdemo:latest'
                }
            }
        }
    }
}
