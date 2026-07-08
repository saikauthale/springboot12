pipeline {

    agent any

    environment {
        IMAGE_NAME = "springboot-demo"
        CONTAINER_NAME = "springboot-container"
        DEPLOY_HOST = "43.205.108.87"
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

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(credentials: ['ssh -o StrictHostKeyChecking=no 172.31.16.152 "hostname']) {
                    sh '''
                    docker save $IMAGE_NAME | bzip2 | \
                    ssh -o StrictHostKeyChecking=no $DEPLOY_HOST '
                    bunzip2 | docker load

                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true

                    docker run -d \
                    --name $CONTAINER_NAME \
                    -p 8080:8080 \
                    $IMAGE_NAME
                    '
                    '''
                }
            }
        }

    }

}
