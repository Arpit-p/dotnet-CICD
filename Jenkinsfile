pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Check out the source code from the Git repository
               git url: 'https://github.com/Arpit-p/dotnet-CICD.git',branch='main'
            }
        }

        stage('Build with Docker') {
            steps {
                // Build the .NET project with Docker
                script {
                    sh 'cd home/ubuntu/webpage '
                    sh 'docker build -t dotnet_CICD .' // Pull your Docker image
                }
            }
        }

        stage('run container to AWS') {
            steps {
                // Deploy the built artifacts to the AWS server
                script {
                    sh 'docker run -d -p 8085:80 --name CICD dotnet_CICD' // Transfer artifacts to AWS server using SCP
                }
            }
        }
    }
}
