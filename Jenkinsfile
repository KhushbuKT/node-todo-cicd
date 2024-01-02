pipeline {
    agent any

    stages {
        stage('Code') {
            steps {
                echo 'This is code stage'
                git url: "https://github.com/KhushbuKT/node-todo-cicd.git", branch:"master" 
            }
        }
        stage('Build') {
            steps {
                echo 'This is build stage'
                sh "docker build -t node-todo-app ."
            }
        }
        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId:"DockerHub", passwordVariable:"DockerHubPass",usernameVariable:"DockerHubUser")]){
                echo 'This is push stage'
                sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                sh "docker tag node-todo-app:latest ${env.DockerHubUser}/node-todo-app:latest"
                sh "docker push ${env.DockerHubUser}/node-todo-app:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'This is deploy stage'
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

