pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/GeethmiUduwana/food-recipe-website-.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t food-recipe-site .'
            }
        }

        stage('Deploy Website') {
            steps {
                sh '''
                docker rm -f food-recipe || true
                docker run -d -p 8081:80 --name food-recipe food-recipe-site
                '''
            }
        }
    }
}
