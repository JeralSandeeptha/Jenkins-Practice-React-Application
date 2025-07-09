pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Ensure this matches the name configured in Jenkins' Global Tool Configuration
        sonarScanner 'SonarScanner'
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

        stage('Run Tests') {
          steps {
            sh 'npm run test'
          }
        }

        stage('Build Project') {
          steps {
            sh 'npm run build'
          }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonarQubeServer') {
                    sh 'sonar-scanner'
                }
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
