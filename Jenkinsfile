pipeline {
    agent any

    environment {
        MAVEN_OPTS = "-Dmaven.repo.local=.m2/repository"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AmanPatne/sem6_honors_fightbooking.git'
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    docker.image('amanpatne/flightbooking:latest').inside("-v ${env.WORKSPACE}/.m2:/root/.m2") {
                        // Clean and package without tests
                        sh 'mvn clean package -DskipTests'

                        // Run tests
                        sh 'mvn test'
                    }
                }
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
        failure {
            echo 'Build failed! Please check the logs.'
        }
        success {
            echo 'Build and tests passed successfully!'
        }
    }
}
