pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = "us-east-1"
        GITHUB_REPO_URL = "https://github.com/anisha16/Cloudformation-Pipeline-demo.git"
        CLOUDFORMATION_FOLDER = "Cloudformation"
        CLOUDFORMATION_SCRIPT_S3 = "${env.CLOUDFORMATION_FOLDER}/s3.yaml"
        SNS_TEMPLATE_PATH = "${env.CLOUDFORMATION_FOLDER}/sns.yaml" // Define the path to sns.yaml
    }
    stages {
        stage("Install yq") {
            steps {
                script {
                    // Install yq
                    sh "sudo apt-get update && sudo apt-get install yq -y"
                }
            }
        }
        stage("Clone Repository") {
            steps {
                git branch: 'main', url: "${env.GITHUB_REPO_URL}"
            }
        }
        stage("Create SNS Topic") {
            steps {
                script {
                    def snsTopicName = sh(script: "cat ${env.SNS_TEMPLATE_PATH} | yq -r '.Parameters[] | select(.ParameterKey == \"TopicName\") | .ParameterValue'", returnStdout: true).trim()
                    withCredentials([aws(credentialsId: 'jenkins-cred', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                        sh "aws cloudformation create-stack --stack-name my-sns-stack --template-body file://${env.SNS_TEMPLATE_PATH} --parameters ParameterKey=TopicName,ParameterValue=${snsTopicName}"
                    }
                }
            }
        }
        stage("Deploy S3 Bucket") {
            steps {
                withCredentials([aws(credentialsId: 'jenkins-cred', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh "aws --version" // Check AWS CLI version
                    sh "aws cloudformation create-stack --stack-name my-s3-stack10 --template-body file://${env.CLOUDFORMATION_SCRIPT_S3} --capabilities CAPABILITY_IAM"
                }
            }
        }
    }
}
