pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Ensure this matches the name configured in Jenkins' Global Tool Configuration
    }

    environment {
        SONAR_TOKEN = credentials('jenkins-sonarqube-token')
        APP_NAME = "jenkins-practice-react-application"
        RELEASE = "1.0.0"
        DOCKER_USER = "jeralsandeeptha"
        DOCKER_PASS = 'dockerhub'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
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
            bat 'npm install'
          }
        }

        stage('Run Tests') {
          steps {
            bat 'npm run test'
          }
        }

        stage('Build Project') {
          steps {
            bat 'npm run build'
          }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube-server') {
                    script {
                        def scannerHome = tool name: 'sonarqube-scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                        bat """
                            ${scannerHome}\\bin\\sonar-scanner.bat ^
                            -Dsonar.projectKey=Jenkins-Practice-React-Application ^
                            -Dsonar.sources=. ^
                            -Dsonar.host.url=http://localhost:9000 ^
                            -Dsonar.login=${env.SONAR_TOKEN}
                        """
                    }
                }
            }
        }
        // stage('SonarQube Analysis') {
        //     steps {
        //         withSonarQubeEnv('sonarqube-server') {
        //             bat '''
        //                 sonar-scanner ^
        //                 -Dsonar.projectKey=Jenkins-Practice-React-Application ^
        //                 -Dsonar.sources=. ^
        //                 -Dsonar.host.url=http://localhost:9000 ^
        //                 -Dsonar.login=%SONAR_TOKEN%
        //             '''
        //         }
        //     }
        // }

        stage('Build & Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        // Login to Docker Hub
                        bat "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
        
                        // Build Docker image
                        def dockerImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
        
                        // Push tagged image
                        dockerImage.push("${IMAGE_TAG}")
        
                        // Push latest tag
                        dockerImage.push("latest")
        
                        // Logout (optional)
                        bat "docker logout"
                    }
                }
            }
        }

        // stage('Quality Gate') {
        //     steps {
        //         // Wait for the quality gate result
        //         timeout(time: 5, unit: 'MINUTES') {
        //             waitForQualityGate abortPipeline: true
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
