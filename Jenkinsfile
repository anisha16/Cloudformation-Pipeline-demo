pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/anisha16/Cloudformation-Pipeline-demo.git'
            }
        }

        stage('Create VPC') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials-id',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                ]]) {
                    sh "/opt/homebrew/bin/aws cloudformation create-stack --stack-name my-vpc-stack --template-body file://cloudformation/vpc.yaml --region us-east-1 --profile aws-jenkins"
                }
            }
        }

        stage('Create Security Group') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials-id',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                ]]) {
                    sh "/opt/homebrew/bin/aws cloudformation create-stack --stack-name my-sg-stack --template-body file://cloudformation/sg.yaml --region us-east-1 --profile aws-jenkins"
                }
            }
        }
    }
}
