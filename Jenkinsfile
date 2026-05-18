pipeline {
    agent any

    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'master',
                url: 'https://github.com/mahi8867/flask-curd.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip3 install --break-system-packages -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'pip3 install --break-system-packages pytest'
                sh 'python3 -m pytest || true'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                    $SCANNER_HOME/bin/sonar-scanner \
                    -Dsonar.projectKey=flask-curd \
                    -Dsonar.projectName=flask-curd \
                    -Dsonar.sources=.
                    '''
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t flask-curd .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh '''
                docker stop flask-curd-container || true
                docker rm flask-curd-container || true
                docker run -d --name flask-curd-container -p 5000:5000 flask-curd
                '''
            }
        }
    }
}

