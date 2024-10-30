pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Specify the Git repository directly
                git branch: 'master', url: 'https://github.com/pradmn/Gitproject.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Clean up any existing Docker containers
                    sh 'docker rm -f $(docker ps -a -q) || true'
                    
                    // Build the Docker image
                    sh 'docker build /home/workspace/test -t staging'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container in detached mode
                    sh 'docker run -d -p 82:80 staging'
                }
            }
        }

        stage('Push Docker Image to Hub') {
            steps {
                script {
                    // Tag the Docker image
                    sh 'docker tag staging prad810/staging:latest'
                    
                    // Push the Docker image to Docker Hub
                    sh 'docker push prad810/staging:latest'
                }
            }
        }
    }

}
