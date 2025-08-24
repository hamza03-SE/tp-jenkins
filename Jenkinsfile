pipeline {
    agent any
    triggers{
        cron('H 11 * * *')
    }
    stages {
        stage('Build') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo Building the application...'
                    sh 'docker build -t $DOCKER_USER/my-python-app:latest .'
                }
            }
        }

        stage('Test') {
            steps {
                sh 'echo Running tests...'
                // Tu peux ajouter des tests ici (par exemple : pytest, etc.)
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo Pushing the Docker image to Docker Hub...'
                    sh 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    sh 'docker push $DOCKER_USER$/my-python-app:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo Deploying the application...'
                sh 'docker pull hamzaerradi03/my-python-app:latest'
                sh 'docker stop my-python-app || exit 0'
                sh 'docker rm my-python-app || exit 0'
                sh 'docker run -d -p 5000:5000 --name my-python-app hamzaerradi03/my-python-app:latest'
            }
        }
    }
}
