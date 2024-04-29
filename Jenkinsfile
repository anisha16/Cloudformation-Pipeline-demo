pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/anisha16/Cloudformation-Pipeline-demo.git'
            }
        }

        stage('Create VPC') {
            steps {
                sh 'aws cloudformation create-stack --stack-name my-vpc-stack --template-body file://cloudformation/vpc.yaml'
            }
        }

        stage('Create Security Group') {
            steps {
                sh 'aws cloudformation create-stack --stack-name my-sg-stack --template-body file://cloudformation/sg.yaml'
            }
        }
    }
}

