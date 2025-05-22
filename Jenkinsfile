pipeline {
    agent any

    environment {
        DOCKER_USER = credentials('docker-username')  // Crée cette variable d'identifiants dans Jenkins
        DOCKER_PASS = credentials('docker-password')  // Crée cette variable aussi
    }

    stages {
        stage('Build') {
            steps {
                bat 'echo Building the application...'
                bat 'docker build -t %DOCKER_USER%/my-python-app:latest .'
            }
        }

        stage('Test') {
            steps {
                bat 'echo Running tests...'
                // Tu peux ajouter des tests ici
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat 'echo Logging into Docker Hub...'
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat 'docker push %DOCKER_USER%/my-python-app:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                bat 'echo Deploying the application...'
                // Ajoute ici la logique SSH vers ton serveur si besoin
            }
        }
    }
}
