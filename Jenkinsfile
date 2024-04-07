pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your version control system (e.g., Git)
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Execute SonarQube analysis
                withSonarQubeEnv('my_sonar_scanner') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage('Build') {
            steps {
                // Build your Java project (e.g., using Maven)
                sh 'mvn clean package'
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
