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
                    // Run commands inside your docker container and mount .m2 for caching
                    docker.image('amanpatne/flightbooking:flightbooking').inside("-v ${env.WORKSPACE}/.m2:/root/.m2") {
                        // Build
                        sh 'mvn clean package -DskipTests'
                        // Test
                        sh 'mvn test'
                    }
                }
            }
        }
    }
}
