pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from the repository
                git 'https://github.com/your/repository.git'
            }
        }
        
        stage('Build') {
            steps {
                // Build the Docker image
                script {
                    docker.build("my-node-app:${env.BUILD_NUMBER}")
                }
            }
        }
        
        stage('Test') {
            steps {
                // Run tests if needed
                sh 'npm test'
            }
        }
        
        stage('Deploy') {
            steps {
                // Deploy the Docker container
                script {
                    docker.withRegistry('https://your-docker-registry.com', 'docker-registry-credentials') {
                        docker.image("my-node-app:${env.BUILD_NUMBER}").push('latest')
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
