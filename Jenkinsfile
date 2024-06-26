pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = "us-east-1"
        GITHUB_REPO_URL = "https://github.com/anisha16/Cloudformation-Pipeline-demo.git"
        CLOUDFORMATION_FOLDER = "Cloudformation"
        CLOUDFORMATION_SCRIPT_S3 = "${env.CLOUDFORMATION_FOLDER}/s3.yaml"
        CLOUDFORMATION_SCRIPT_SNS = "${env.CLOUDFORMATION_FOLDER}/sns.yaml"
    }
    stages {
        stage("Clone Repository") {
            steps {
                git branch: 'main', url: "${env.GITHUB_REPO_URL}"
            }
        }
        stage("Create SNS Topic") {
            steps {
                script {
                    withCredentials([aws(credentialsId: 'jenkins-cred', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                        sh "aws cloudformation create-stack --stack-name my-sns-stack2 --template-body file://${env.CLOUDFORMATION_SCRIPT_SNS}"
                    }
                }
            }
        }
        stage("Deploy S3 Bucket") {
            steps {
                withCredentials([aws(credentialsId: 'jenkins-cred', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh "aws --version" // Check AWS CLI version
                    sh "aws cloudformation create-stack --stack-name my-s3-stack14 --template-body file://${env.CLOUDFORMATION_SCRIPT_S3} --capabilities CAPABILITY_IAM"
                }
            }
        }
    }
}
