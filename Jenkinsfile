pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application'
            }
        }

        stage('Test') {
            steps {
                echo 'Running automated tests'
            }
        }

        stage('Package') {
            steps {
                sh 'docker build -t week9-app .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f week9-container || true
                    docker run -d --name week9-container -p 8081:80 week9-app
                '''
            }
        }

    }
}
