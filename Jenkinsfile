pipeline {
    agent any
    
    environment {
        SONAR_LOGIN = credentials('sonar-login') // SonarQube login credentials ID
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your version control system (e.g., Git)
                git 'https://github.com/your/repository.git'
            }
        }
        
        stage('Build') {
            steps {
                // Build your Java project (e.g., using Maven)
                sh 'mvn clean package'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                // Execute SonarQube analysis
                withSonarQubeEnv('SonarQubeServer') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
    
    post {
        always {
            // Publish SonarQube analysis results
            publishIssues issuesMode: 'sonarqube'
            // You can add more post-build actions here as needed
        }
    }
}
