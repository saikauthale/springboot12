pipeline {

    agent any

    tools {

        maven 'Maven3'

    }

    stages {

        stage('Clone') {

            steps {

                git branch: 'main',
                url: 'https://github.com/saikauthale/springboot12.git'

            }

        }

        stage('Build') {

            steps {

                sh 'mvn clean package'

            }

        }

        stage('Docker Build') {

            steps {

                sh 'docker build -t springboot-app .'

            }

        }

        stage('Docker Tag') {

            steps {

                sh 'docker tag springboot-app username/springboot-app:latest'

            }

        }

        stage('Docker Push') {

            steps {

                withCredentials([usernamePassword(
                credentialsId: 'dockerhub',
                usernameVariable: 'USER',
                passwordVariable: 'PASS')]) {

                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push username/springboot-app:latest
                    '''

                }

            }

        }

        stage('Deploy') {

            steps {

                sh '''
                docker stop springboot || true
                docker rm springboot || true

                docker run -d \
                --name springboot \
                -p 8080:8080 \
                username/springboot-app:latest
                '''

            }

        }

    }

}

