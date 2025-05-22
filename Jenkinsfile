pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat 'echo Building the application...'
                    bat 'docker build -t %DOCKER_USER%/my-python-app:latest .'
                }
            }
        }

        stage('Test') {
            steps {
                bat 'echo Running tests...'
                // Ajouter vos tests ici si nécessaire
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat 'echo Pushing the Docker image to Docker Hub...'
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat 'docker push %DOCKER_USER%/my-python-app:latest'
                }
            }
        }

       
        stage('Deploy') {
    steps {
        bat 'echo Deploying the application...'
        bat 'docker pull hamzaerradi03/my-python-app:latest'
        bat 'docker stop my-python-app || exit 0'
        bat 'docker rm my-python-app || exit 0'
        bat 'docker run -d -p 5000:5000 --name my-python-app hamzaerradi03/my-python-app:latest'
    }
}

    }
}
