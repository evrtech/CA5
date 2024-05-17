pipeline {
    agent any
    
    stages {
        stage('Docker Login') {
            steps {
                script {
                    // Extract username and password from credentials
                    def creds = credentials('autom8ers-dockerhub')
                    def username = creds.getUsername()
                    def password = creds.getPassword()
                    
                    // Use username and password to login to Docker
                    sh "echo ${password} | docker login --username ${username} --password-stdin"
                }
            }
        }
        
     //adding frontend   
        stage('Build and Push Frontend Docker Image') {
            steps {
                dir('Frontend') {
                    script {
                        // Build the frontend Docker image
                        sh 'docker build -t autom8ers/frontend-image:latest .'
                        // Push the frontend Docker image to Docker Hub
                        sh 'docker push autom8ers/frontend-image:latest'
                    }
                }
            }
        }
        
        stage('Build and Push Backend Docker Image') {
            steps {
                dir('Backend') {
                    script {
                        // Build the backend Docker image
                        sh 'docker build -t autom8ers/backend-image:latest .'
                        // Push the backend Docker image to Docker Hub
                        sh 'docker push autom8ers/backend-image:latest'
                    }
                }
            }
        }
        
        stage('Docker Logout') {
            steps {
                sh 'docker logout'
            }
        }
    }
}
