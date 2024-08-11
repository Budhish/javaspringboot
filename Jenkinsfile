pipeline {
    agent any
        options {
        timestamps() // Add this line to enable timestamps in  console o/p 
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/dev1']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-credentials-java', url: 'https://github.com/Budhish/javaspringboot.git']])
            }
        }

        stage('code build') {
            steps {
                sh """
                mvn install
                """
            }
        }

         stage('dockerbuild') {
            steps {
                sh """
                docker build -t rs-image:1.0 .
                """
            }
        }
    }
}


