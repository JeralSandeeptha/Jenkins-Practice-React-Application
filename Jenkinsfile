pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Ensure this matches the name configured in Jenkins' Global Tool Configuration
    }

    environment {
        SONAR_TOKEN = credentials('jenkins-sonarqube-token')
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
                withSonarQubeEnv('sonarqube-server') {
                    sh """
                        sonar-scanner \
                        -Dsonar.projectKey=Jenkins-Practice-React-Application \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://host.docker.internal:9000 \
                        -Dsonar.login=$SONAR_TOKEN
                    """
                }
            }
        }

        // stage('SonarQube Analysis') {
        //     steps {
        //         script {
        //             withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
        //                 sh 'sonar-scanner'
        //             }
        //         }
        //     }
        // }
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
