pipeline {
    agent {label "agent-1"}

    stages {
        stage("Code") {
            steps {
                git url: "https://github.com/Rishabh077777/django-notes-app.git" , branch:"main"
            }
        }
        
        stage("Install packages") {
            steps {
                sh '''
                sudo apt-get update -y
                sudo apt-get install docker.io -y
                sudo systemctl enable docker --now
                sudo systemctl status docker
                sudo usermod -aG docker ubuntu
                newgrp docker
                docker ps
                '''
            }
        }
        
        stage("Build") {
            steps {
                sh '''
                docker build -t notes-app .
                '''
            }
        }
        
        stage("Test") {
            steps {
                sh "mkdir -p cloud"
            }
        }
        
        stage("Deploy") {
            steps {
                sh '''
                docker run -d -p 8000:8000 notes-app:latest
                '''
            }
        }
    }
}
