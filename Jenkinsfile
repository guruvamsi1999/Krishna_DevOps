pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/guruvamsi1999/Krishna_DevOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Lint') {
            steps {
                sh 'pylint --output-format=parseable your-python-file.py'
            }
        }

        stage('Unit Test') {
            steps {
                sh 'python -m unittest discover -s tests -p "test_*.py"'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:${env.BUILD_NUMBER} .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    sh 'docker push myregistry/myapp:${env.BUILD_NUMBER}'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Your deployment steps here
            }
        }
    }
}
