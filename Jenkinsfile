pipeline {
    agent any

    stages {
        stage('Create VPC') {
            steps {
                script {
                    withCredentials([[
                        $class: 'AmazonWebServicesCredentialsBinding',
                        credentialsId: 'jenkins-aws',
                        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                    ]]) {
                        sh "/opt/homebrew/bin/aws cloudformation create-stack --stack-name my-vpc-stack --template-body file://cloudformation/vpc.yaml --region us-east-1 --profile jenkins-aws"
                    }
                }
            }
        }

        stage('Create Security Group') {
            steps {
                script {
                    withCredentials([[
                        $class: 'AmazonWebServicesCredentialsBinding',
                        credentialsId: 'jenkins-aws',
                        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                    ]]) {
                        sh "/opt/homebrew/bin/aws cloudformation create-stack --stack-name my-sg-stack --template-body file://cloudformation/sg.yaml --region us-east-1 --profile jenkins-aws"
                    }
                }
            }
        }
    }
}
