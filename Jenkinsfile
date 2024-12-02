pipeline {
    agent any
    
    stages{
        stage('Code'){
            steps {
                git url: 'https://github.com/kannancloud001/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build and Test'){
            steps {
                sh 'docker build . -t trainwithshubham/node-todo-app-cicd:latest' 
            }
        }
        stage('Login and Push Image'){
            steps {
                echo 'logging in to docker hub and pushing image..'
                withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dockerHubPassword', usernameVariable:'dockerHubUser')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push trainwithshubham/node-todo-app-cicd:latest"
                }
            }
        }
        stage('Deploy'){
            steps {
                sh 'docker compose up -d'
            }
        }
    }
}
