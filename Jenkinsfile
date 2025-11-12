pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t myapp:latest .'
            }
        }

        stage('Test Container') {
            steps {
                bat 'docker run --rm myapp:latest'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                    docker stop myapp || exit 0
                    docker rm myapp || exit 0
                    docker run -d --name myapp myapp:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

