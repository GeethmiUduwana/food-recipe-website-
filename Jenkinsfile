pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "food-recipe-site"
    }
    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-pat',  // HTTPS credential in Jenkins
                    url: 'https://github.com/GeethmiUduwana/food-recipe-website-.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Deploy Website') {
            steps {
                bat '''
                docker rm -f food-recipe || echo "No container to remove"
                docker run -d -p 8081:80 --name food-recipe %DOCKER_IMAGE%
                '''
            }
        }
    } // end stages
} // end pipeline
