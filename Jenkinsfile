pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Ensure this matches the name configured in Jenkins' Global Tool Configuration
    }

    stages {
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout from SCM') {
          steps {
            git branch: 'master', url: 'https://github.com/JeralSandeeptha/Jenkins-Practice-React-Application.git'
          }
        }

        stage('Install Dependencies') {
          steps {
            sh 'npm install'
          }
        }
    }

    post {
        success {
            echo 'Build succeeded weddo!'
        }
        failure {
            echo 'Build failed modayo!'
        }
    }
}
