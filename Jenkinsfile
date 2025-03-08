pipeline{
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials')
        DOCKER_IMAGE = 'todo-application-image:latest'
    }
    stages{
        stage('Clone Repository'){
            steps{
                script {
                    sh 'git clone https://github.com/pratik-tonage/todo-application.git'
                }
            }        
        }
        stage('Build with Maven'){
            steps{
                script {
                     sh 'mvn clean package -DskipTests'
                }
            }   
        }
        stage('Build Docker Image'){
            steps{
                script {
                     sh 'docker build -t todo-application-image:latest .'
                }
            }
        }       
        stage('Push Docker Images to Docker Hub'){
            steps{
                script {
                    withCredentials([usernamePassword(credentialsID: DOCKER_HUB_CREDENTIALS, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push $DOCKER_IMAGE'
                    }
                }
            }
        }    
        stage('Deploy with Docker Compose'){
            steps{
                script {
                     sh 'docker compose up -d'
                }
            }    
        }    
        stage('Verify Services'){
            steps{
                script {
                     sh 'docker ps'
                }
            }      
        }
        stage('Clean Workspace'){
            steps{
                script {
                     sh 'rm -rf *'
                }
            }    
        }
    }        
}        
        
            
            
            
            
            
            
            
            
            
        
