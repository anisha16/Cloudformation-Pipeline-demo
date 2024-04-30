pipeline {
    agent any

    stages {
        stage('Create VPC') {
            steps {
                script {
                    sh """
                        /opt/homebrew/bin/aws cloudformation create-stack \
                        --stack-name my-vpc-stack \
                        --template-body file://cloudformation/vpc.yaml \
                        --region us-east-1 \
                        --profile jenkins
                    """
                }
            }
        }

        stage('Create Security Group') {
            steps {
                script {
                    sh """
                        /opt/homebrew/bin/aws cloudformation create-stack \
                        --stack-name my-sg-stack \
                        --template-body file://cloudformation/sg.yaml \
                        --region us-east-1 \
                        --profile jenkins
                    """
                }
            }
        }
    }
}
