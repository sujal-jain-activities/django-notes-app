pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'code clone'
                git branch: 'main', url: 'https://github.com/sujal-jain-activities/django-notes-app.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building code'
                sh 'docker build -t notes-app .' 
            }
        }
        stage('Push to dockerhub') {
            steps {
                echo 'Dockerhub'
                withCredentials([usernamePassword(credentialsId: 'dockerhub',passwordVariable: 'dockerhubpass',usernameVariable: 'dockerhubuser')]){
                sh 'docker login -u ${dockerhubuser} -p ${dockerhubpass}'
                sh 'docker tag notes-app ${dockerhubuser}/notes-app:latest'
                sh 'docker push ${dockerhubuser}/notes-app:latest'
                }
            }
        }
        stage('Deployment') {
            steps {
                echo 'Deploying'
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
