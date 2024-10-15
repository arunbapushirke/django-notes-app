pipeline {
    agent {
        node {
            label 'dev'
        }
    }
    
    stages {
        stage('clone code') {
            steps {
                git url: 'https://github.com/arunbapushirke/django-notes-app.git', branch: "main"
                echo 'This is Code Stage'
                 }
            }
            stage('build') {
            steps {
                sh "docker build -t notes-app-jenkins:latest . "
                echo 'This is Code Stage'
                 }
            }
            stage('push to Docker Hub'){
            steps {
                echo "image pushed to docker hub"
                withCredentials(
                    [usernamePassword(
                        credentialsId: "jenkinsDockerHub",
                        passwordVariable: "dockerHubPass",
                        usernameVariable: "dockerHubUser" 
                        )
                    ]
                    ){
                    sh "docker image tag notes-app-jenkins:latest ${env.dockerHubUser}/notes-app-jenkins:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/notes-app-jenkins:latest"
                    }
            }
            }
            stage('deploy') {
            steps {
                    sh "docker compose up -d"
                 }
            }
        }

    }
