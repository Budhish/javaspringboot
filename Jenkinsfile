pipeline {
    agent any
        options {
        timestamps() // Add this line to enable timestamps
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/dev1']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-credentials-java', url: 'https://github.com/Budhish/javaspringboot.git']])
            }
        }
    }
}
   

