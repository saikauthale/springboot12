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

