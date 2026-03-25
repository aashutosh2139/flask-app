pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/aashutosh2139/flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    sh '''
                    if [ "$(docker ps -q -f name=flask)" ]; then
                        docker stop flask
                        docker rm flask
                    fi
                    '''
                }
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 5001:5000 --name flask flask-app'
            }
        }
    }
}
