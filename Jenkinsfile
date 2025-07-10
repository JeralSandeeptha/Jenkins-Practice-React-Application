pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Ensure this matches the name configured in Jenkins' Global Tool Configuration
    }

    // environment {
    //     SONAR_TOKEN = credentials('jenkins-sonarqube-token')
    //     APP_NAME = "jenkins-practice-react-application"
    //     RELEASE = "1.0.0"
    //     DOCKER_USER = "jeralsandeeptha"
    //     DOCKER_PASS = 'dockerhub'
    //     IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
    //     IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    // }

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

        // stage('Run Tests') {
        //   steps {
        //     sh 'npm run test'
        //   }
        // }

        // stage('Build Project') {
        //   steps {
        //     sh 'npm run build'
        //   }
        // }

        // stage('SonarQube Analysis') {
        //     steps {
        //         withSonarQubeEnv('sonarqube-server') {
        //             sh """
        //                 sonar-scanner \
        //                 -Dsonar.projectKey=Jenkins-Practice-React-Application \
        //                 -Dsonar.sources=. \
        //                 -Dsonar.host.url=http://host.docker.internal:9000 \
        //                 -Dsonar.login=$SONAR_TOKEN
        //             """
        //         }
        //     }
        // }

        // stage('Build & Push Docker Image') {
        //   steps {
        //     script {
        //         docker.withRegistry('', DOCKER_PASS) {
        //             docker_image = docker.build "${IMAGE_NAME}"
        //         }
                
        //         docker.withRegistry('', DOCKER_PASS) {
        //             docker_image.push("${IMAGE_TAG}")
        //             docker_image.push('latest')
        //         }
        //     }
        //   }
        // }

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
