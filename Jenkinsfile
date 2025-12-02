pipeline {
    agent any

    stages {
        stage('Clone repo') {
            steps {
                git branch: 'main', url: 'https://github.com/shelo0/sample-app.git'
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    docker build -t sampleapp:latest .
                '''
            }
        }

        stage('Docker Run') {
            steps {
                sh '''
                    docker stop samplerunning || true
                    docker rm samplerunning || true
                    docker run -d --name samplerunning -p 5050:5050 sampleapp:latest
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh '''
                    sleep 3
                    curl -i http://localhost:5050/
                '''
            }
        }
    }
}
