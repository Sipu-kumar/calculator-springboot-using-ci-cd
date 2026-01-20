pipeline {
    agent any

    tools {
        jdk 'JDK-17'
        maven 'Maven-3.9'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sipu-kumar/calculator-springboot.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t calculator-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker stop calculator-container || exit 0
                docker rm calculator-container || exit 0
                docker run -d -p 8080:8080 --name calculator-container calculator-app
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Calculator App deployed successfully using Docker on Windows'
        }
        failure {
            echo '❌ Jenkins Pipeline failed'
        }
    }
}
