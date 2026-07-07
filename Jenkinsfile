pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/saikauthale/springboot12.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
}

