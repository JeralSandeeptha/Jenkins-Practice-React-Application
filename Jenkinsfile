pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Ensure this matches the name configured in Jenkins' Global Tool Configuration
    }

    environment {
        NPM_CONFIG_LOGLEVEL = 'warn' // Optional: Customize NPM log level
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clone the repository
                git url: 'https://github.com/JeralSandeeptha/Jenkins-Practice-React-Application.git', branch: 'master'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node.js dependencies
                sh 'npm install'
            }
        }

        stage('Build Project') {
            steps {
                // Build the Node.js project (adjust this command for your project)
                sh 'npm run build'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive build artifacts, if any
                archiveArtifacts artifacts: 'dist/**/*', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh 'npm install -g serve'
                sh 'serve -s /var/jenkins_home/workspace/cicd-pipeline/dist -l 3000 &'
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
