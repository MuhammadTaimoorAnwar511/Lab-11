pipeline {

    agent any

    tools {nodejs "nodejs_jenkins"} 
    
    stages {
        
        stage('Checkout') {
            steps {
                git 'https://github.com/huzi0906/jenkins-practice.git'
            }
        }

        stage('Dependency Installation') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Run Docker Image') {
            steps {
                sh 'docker build -t jenkins-practice .'
                sh "docker run -d -p 3000:3000 jenkins-practice"
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push jenkins-practice"
            }
        }
    }
}
