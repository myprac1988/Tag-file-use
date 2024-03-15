pipeline {
    agent any
    environment {
            AWS_ACCOUNT_ID="339712930803"
            AWS_DEFAULT_REGIOS="ap-south-1"
            IMAGE_REPO_NAME="myprac"
            IMAGE_TAG="v10.1"
            REPOSITORY_URL="public.ecr.aws/q3w8l9w9/myprac"
    }
    
    stages {
        stage('SCM Checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-myprac', url: 'https://github.com/myprac1988/Dockerfile.git'
            }
        }
        stage('Login to ECR') {
            steps {
                sh 'aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/q3w8l9w9'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myprac:${IMAGE_TAG} .'
            }
        }
        stage('Docker tag image') {
            steps {
                sh 'docker tag myprac:${IMAGE_TAG} public.ecr.aws/q3w8l9w9/myprac:${IMAGE_TAG}'
            }
        }
        stage('Docker push image') {
            steps {
                sh 'docker push public.ecr.aws/q3w8l9w9/myprac:${IMAGE_TAG}'
            }
        }
    }
}
