pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main' , url: 'https://github.com/anisha16/Cloudformation-Pipeline-demo.git'
            }
        }

        stage('Create VPC') {
            steps {
		sh '/opt/homebrew/bin/aws cloudformation create-stack --stack-name my-vpc-stack --template-body file://cloudformation/vpc.yaml --region us-east-1'
            }
        }

        stage('Create Security Group') {
            steps {
                sh '/opt/homebrew/bin/aws cloudformation create-stack --stack-name my-sg-stack --template-body file://cloudformation/sg.yaml --region us-east-1'
            }
        }
    }
}

