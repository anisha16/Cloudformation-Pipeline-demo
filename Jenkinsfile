pipeline {
    agent any
    
    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        AWS_PROFILE = 'new-profile'
    }

    stages {
        stage('Deploy VPC') {
            steps {
                script {
                    sh 'aws cloudformation create-stack --stack-name my-vpc-stack --template-body file://cloudformation/vpc.yaml'
                }
            }
        }

        stage('Deploy S3 Bucket') {
            steps {
                script {
                    sh 'aws cloudformation create-stack --stack-name my-s3-stack --template-body file://cloudformation/s3.yaml'
                }
            }
        }
    }
}
