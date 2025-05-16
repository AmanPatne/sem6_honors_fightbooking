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
                    // Convert Windows path (e.g. C:\Users\lenovo\workspace) to Linux style /c/Users/lenovo/workspace
                    def workspace = env.WORKSPACE
                    def containerWorkspace = workspace.replaceAll('\\\\', '/') // backslashes to forward slashes
                                                      .replaceFirst('^([A-Za-z]):', '/$1') // drive letter C: -> /C
                                                      .toLowerCase() // lowercase drive letter

                    docker.image('amanpatne/flightbooking:latest').inside("-v ${workspace}:${containerWorkspace} -v ${workspace}/.m2:/root/.m2 -w ${containerWorkspace}") {
                        sh 'mvn clean package -DskipTests'
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
