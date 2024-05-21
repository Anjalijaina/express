pipeline {
    agent any

    triggers {
        pollSCM('* * * * *') // Polls the SCM every minute; adjust to your needs
    }

    environment {
        DOCKER_IMAGE = 'hello-world-app'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install dependencies using npm
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Run a dummy test
                sh 'echo "Running dummy tests"'
                // You can add actual test commands here
                // sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    //sh 'sudo visudo'
                     sh 'sudo chmod 777 /var/run/docker.sock'

                    sh 'sudo systemctl start jenkins'

                    sh 'ls -l $WORKSPACE'
                  
                    
                    // Build the Docker image
                    sh 'sudo docker build -t ${DOCKER_IMAGE} .'
                }
            }
        }
    }

    post {
        always {
            // Clean up the workspace after the build
            cleanWs()
        }
    }
}
