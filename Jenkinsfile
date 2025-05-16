pipeline {
    agent {
        docker {
            image 'maven:3.8.5-openjdk-17'
            args '-v ${WORKSPACE}/.m2:/root/.m2' // Use local Maven cache
        }
    }

    environment {
        MAVEN_OPTS = "-Dmaven.repo.local=.m2/repository"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AmanPatne/sem6_honors_fightbooking.git'
            }
        }

        stage('Build') {
            steps {
                dir('Flightbooking') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Test') {
            steps {
                dir('Flightbooking') {
                    sh 'mvn test'
                }
            }
        }
    }
}
