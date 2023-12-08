pipeline {
    agent any
    environment {
        GIT_CREDENTIALS = credentials('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')
        SONARQUBE_SCANNER_HOME = tool 'SonarQubeScanner'
    }
    stages {
        stage('Checkout') {
            steps { 
                script {
                    git credentialsId: 'your-git-credentials-id', url: 'https://github.com/Arpit-p/dotnet-CICD.git', branch: 'main'
                }
            }
        }

        stage('Build with Docker') {
            steps {
                script {
                    sh 'docker build -t dotnet-cicd .' // Build Docker image
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('SonarQubeServer') {
                        sh 'dotnet sonarscanner begin'
                        sh 'dotnet build'
                        sh 'dotnet sonarscanner end /d:sonar.login'
                    }
                }
            }
        }

        stage('Deploy to AWS') {
            steps {
                sh 'docker run -d -p 8087:80 dotnet-cicd'
            }
        }

        // Other stages in your pipeline if needed
    }
}
