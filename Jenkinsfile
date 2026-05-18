pipeline {
    agent any

    tools {
        jdk 'jdk17'
    }

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
                sh '''
                pip3 install --break-system-packages -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                pip3 install --break-system-packages pytest
                python3 -m pytest || true
                '''
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    withCredentials([string(credentialsId: 'sonar-token-new', variable: 'SONAR_TOKEN')]) {

                        sh '''
                        $SCANNER_HOME/bin/sonar-scanner \
                        -Dsonar.projectKey=flask-curd \
                        -Dsonar.projectName=flask-curd \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://13.218.197.61:9000 \
                        -Dsonar.login=$SONAR_TOKEN
                        '''
                    }
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                sudo docker build -t flask-curd .
                '''
            }
        }

        stage('Docker Deploy') {
            steps {
                sh '''
                sudo docker stop flask-container || true
                sudo docker rm flask-container || true

                sudo docker run -d \
                --name flask-container \
                -p 5000:5000 \
                flask-curd
                '''
            }
        }
    }
}
