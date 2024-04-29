pipeline {
    agent any
    
    options {
        skipDefaultCheckout(true)
        ansiColor('xterm')
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                // Cloning the repository
                script {
                    dir('Cloudformation-Pipeline-demo') {
                        git branch: 'main',
                        credentialsId: 'GITHUB_ACCESS_KEY',
                        url: 'git@github.com:anisha16/Cloudformation-Pipeline-demo.git'
                    }
                }
            }
        }
        stage('Create S3 Bucket') {
            steps {
                script {
                    dir('Cloudformation-Pipeline-demo/cloudformation') {
                        sh 'aws cloudformation deploy --stack-name my-s3-bucket-stack --template-file s3.yaml --capabilities CAPABILITY_IAM'
                    }
                }
            }
        }
        stage('Create VPC and Subnets') {
            steps {
                script {
                    dir('Cloudformation-Pipeline-demo/cloudformation') {
                        sh 'aws cloudformation deploy --stack-name my-vpc-subnets-stack --template-file vpc.yaml --capabilities CAPABILITY_IAM'
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs() // Clean workspace after pipeline execution
        }
    }
}

