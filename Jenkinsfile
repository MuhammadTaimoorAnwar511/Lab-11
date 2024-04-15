pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'myapp:latest'
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'
        DOCKER_REGISTRY = 'https://index.docker.io/v1/'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/MuhammadTaimoorAnwar511/Lab-11.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Adjust this step according to your project's dependency manager
                // For example, if it's a Node.js project, you might use `npm install`
                // If it's a Python project, you might use `pip install -r requirements.txt`
                echo 'Assuming Node.js setup: Running npm install'
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Run Docker Image') {
            steps {
                // Adjust port mappings based on your application's needs
                echo 'Running Docker container on port 80'
                sh "docker run -d -p 80:80 ${DOCKER_IMAGE}"
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry(DOCKER_REGISTRY, DOCKER_CREDENTIALS_ID) {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
