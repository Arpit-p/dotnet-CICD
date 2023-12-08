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
                    git credentialsId: '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', url: 'https://github.com/Arpit-p/dotnet-CICD.git', branch: 'main'
                }
            }
        }

        // stage('Build with Docker') {
        //     steps {
        //         script {
        //             sh 'docker build -t dotnet-cicd .' // Build Docker image
        //         }
        //     }
        // }

       stage('SonarQube Analysis') {
    steps {
        script {
            // Use SonarQube credentials
            withCredentials([string(credentialsId: '1', variable: 'SONAR_TOKEN')]) {
                // Execute SonarScanner commands
                sh "dotnet sonarscanner begin /k:'ec18d7ccc6c967f19c225f8994a13204c6c34e24' /d:sonar.host.url='http://sonarqube-server:9000' /d:sonar.login=\${SONAR_TOKEN}"
                sh 'dotnet build'
                sh "dotnet sonarscanner end /d:sonar.login=\${SONAR_TOKEN}"
            }
        }
    }
}

        // stage('Deploy to AWS') {
        //     steps {
        //         sh 'docker run -d -p 8087:80 dotnet-cicd'
        //     }
        // }

        // Other stages in your pipeline if needed
    }
}
