pipeline {
    agent any
     tools {
        // already Defined the Maven tool to use from Jenkins as a plugin insted of directly installingon server
        maven 'mvn'  // mvn is what we named in tools configuration in Jenkins
    }
    stages {
        stage('Build') {
            steps {
                // Build your project (e.g., Maven)
                sh 'mvn clean package'
            }
        }

        stage('removal') {
            steps {
                // removal of prev containers and images
                sh 'docker rm -f mynewcontainer'
                sh 'docker rmi `docker images`|| echo "Command 3 failed with exit code $?"'
            }
        }

        stage('Docker Build') {
            steps {
                // Build a Docker image
                sh 'docker build -t image-name:version .'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the Docker image to your environment (e.g., Kubernetes, Docker Swarm)
                sh 'docker run -d -p 8081:8080 --name mynewcontainer image-name:version'
            }
        }
    }
    
    post {
        success {
            // Actions to take on a successful pipeline run
            echo 'Pipeline completed successfully'
        }
        failure {
            // Actions to take on a failed pipeline run
            echo 'Pipeline failed'
        }
    }
}
