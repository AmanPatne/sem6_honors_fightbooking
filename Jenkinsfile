pipeline {
    agent any

    tools {
        maven 'Maven 3.9.5'
        jdk 'Java 17'
    }

    environment {
        MAVEN_OPTS = "-Dmaven.repo.local=.m2/repository"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/AmanPatne/sem6_honors_fightbooking.git'
            }
        }

        stage('Build') {
            steps {
                dir('Flightbooking') {
                    bat 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Test') {
            steps {
                dir('Flightbooking') {
                    bat 'mvn test'
                }
            }
        }
    }
}
