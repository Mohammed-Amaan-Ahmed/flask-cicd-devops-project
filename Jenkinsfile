pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-south-2'
        ECR_REPO = '432839260003.dkr.ecr.ap-south-2.amazonaws.com/flask-devops-app'
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-app:${BUILD_NUMBER} .'
            }
        }

        stage('Tag Docker Image') {
            steps {
                sh '''
                docker tag flask-app:${BUILD_NUMBER} $ECR_REPO:${BUILD_NUMBER}
                '''
            }
        }

        stage('Login to ECR') {
            steps {
                withCredentials([
                    string(credentialsId: 'NEW_AWS_ACCESS_KEY_ID', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'NEW_AWS_SECRET_ACCESS_KEY', variable: 'AWS_SECRET_ACCESS_KEY')
                ]) {
                    sh '''
                    aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
                    aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
                    aws configure set default.region $AWS_REGION

                    aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin 432839260003.dkr.ecr.ap-south-2.amazonaws.com
                    '''
                }
            }
        }

        stage('Push Image to ECR') {
            steps {
                sh '''
                docker push $ECR_REPO:${BUILD_NUMBER}
                '''
            }
        }
    }

    post {

        success {
            emailext(
                to: 'amaanahmed4463@gmail.com',
                subject: "SUCCESS: ${JOB_NAME} Build #${BUILD_NUMBER}",
                body: """
Build Status: SUCCESS

Job Name: ${JOB_NAME}
Build Number: ${BUILD_NUMBER}

Build URL:
${BUILD_URL}
"""
            )
        }

        failure {
            emailext(
                to: 'amaanahmed4463@gmail.com',
                subject: "FAILED: ${JOB_NAME} Build #${BUILD_NUMBER}",
                body: """
Build Status: FAILED

Job Name: ${JOB_NAME}
Build Number: ${BUILD_NUMBER}

Build URL:
${BUILD_URL}
"""
            )
        }
    }
}