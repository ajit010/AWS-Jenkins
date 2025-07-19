pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        AWS_REGION = 'us-east-1'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/yourusername/aws-jenkins-demo.git'
            }
        }
        stage('Create S3 Bucket') {
            steps {
                sh '''
                  aws s3 mb s3://jenkins-demo-bucket-${BUILD_ID} --region $AWS_REGION
                '''
            }
        }
        stage('Upload File') {
            steps {
                sh '''
                  echo "Hello from Jenkins AWS pipeline!" > message.txt
                  aws s3 cp message.txt s3://jenkins-demo-bucket-${BUILD_ID}/
                '''
            }
        }
    }
}
