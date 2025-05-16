pipeline {
    agent {
        docker {
            image 'amanpatne/flightbooking:flightbooking'
            args "-v ${env.WORKSPACE.replaceAll('\\\\','/') }:/workspace -w /workspace -v ${env.WORKSPACE.replaceAll('\\\\','/')}/.m2:/root/.m2"
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
