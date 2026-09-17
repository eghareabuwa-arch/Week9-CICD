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
                sh 'docker build -t week9-app:v3 .'
            }
        }

        stage('Security Scan') {
    steps {
        sh '''
        echo "Running Trivy security scan"

        docker run --rm \
        -v /var/run/docker.sock:/var/run/docker.sock \
        aquasec/trivy image \
        --scanners vuln \
        --timeout 15m \
        week9-app:v3
        '''
    }
}

        stage('Deploy') {
            steps {
                sh '''
                docker rm -f week9-container || true
                docker run -d --name week9-container -p 8081:80 week9-app:v3
                '''
            }
        }
    }
}
