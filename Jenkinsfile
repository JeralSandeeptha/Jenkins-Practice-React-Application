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
