pipeline {
    agent any
    options {
        timestamps() // Add this line to enable timestamps in console output
    }
    environment {
        // Define AWS ECR variables
        AWS_ACCOUNT_ID = '381491906321'   
        AWS_REGION = 'us-east-1' 
        ECR_REPOSITORY = 'rulestudio-javapp'
        IMAGE_TAG = '1.0'
        IMAGE_NAME = 'rs-image'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/dev1']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-credentials-java', url: 'https://github.com/Budhish/javaspringboot.git']])
            }
        }

        stage('Code Build') {
            steps {
                sh """
                mvn install
                """
            }
        }

        stage('Docker Build') {
            steps {
                sh """
                docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                """
            }
        }

        stage('Push to ECR') {
            steps {
                script {
                    // Authenticate Docker to the ECR registry
                    sh """
                    aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com
                    """

                    // Tag the Docker image
                    sh """
                    docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_REPOSITORY}:${IMAGE_TAG}
                    """

                    // Push the Docker image to ECR
                    sh """
                    docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_REPOSITORY}:${IMAGE_TAG}
                    """
                }
            }
        }
    }
    post {
        success {
            echo 'Build and push to ECR succeeded!'
        }
        failure {
            echo 'Build or push to ECR failed.'
        }
    }
}


