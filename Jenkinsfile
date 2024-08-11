pipeline {
    agent any
        options {
        timestamps() // Add this line to enable timestamps
    }

    parameters {
        booleanParam(name: 'autoApprove', defaultValue: false, description: 'Automatically run apply after generating plan?')
        choice(name: 'action', choices: ['apply', 'destroy'], description: 'Select the action to perform')
    }

    environment {
        AWS_ACCESS_KEY_ID     = credentials('access-key')
        AWS_SECRET_ACCESS_KEY = credentials('access-key')
        AWS_DEFAULT_REGION    = 'us-east-1'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/dev1']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-credentials-java', url: 'https://github.com/Budhish/javaspringboot.git']])
            }
        }
    }
}
   

