pipeline {
    agent any

    environment {
        IMAGE = 'amanpatne/flightbooking:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AmanPatne/sem6_honors_fightbooking'
            }
        }

        stage('Build') {
            steps {
                script {
                    echo """
                    docker run --rm -v ${pwd()}:/app -w /app ${IMAGE} mvn clean package -DskipTests
                    """
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo """
                    docker run --rm -v ${pwd()}:/app -w /app ${IMAGE} mvn test
                    """
                }
            }
        }
    }
}
