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
                sh 'pip3 install pytest'
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
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://13.218.197.61:9000
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
                docker stop flask-app || true
                docker rm flask-app || true
                docker run -d -p 5000:5000 --name flask-app flask-curd
                '''
            }
        }
    }
}
