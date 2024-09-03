pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                sh './gradlew build' // Use Gradle wrapper to build the project
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                sh './gradlew test' // Use Gradle wrapper to run tests
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running code analysis...'
                sh './gradlew sonarqube' // Use Gradle wrapper for SonarQube analysis
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Add command for security scan, adjust based on your tool
                sh 'dependency-check --project MyProject --scan ./build' // Example command, adjust as needed
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                sh 'scp -r ./build/libs/your-app.jar user@staging-server:/path/to/staging' // Adjust based on your deployment tool
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Add command for running integration tests on staging
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                sh 'scp -r ./build/libs/your-app.jar user@production-server:/path/to/production' // Adjust based on your deployment tool
            }
        }
    }
    post {
        success {
            mail to: 'samshertamang08@gmail.com',
                 subject: "SUCCESS: ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                 body: "Good news, ${env.JOB_NAME} build ${env.BUILD_NUMBER} was successful!"
        }
        failure {
            mail to: 'samshertamang08@gmail.com',
                 subject: "FAILURE: ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                 body: "Bad news, ${env.JOB_NAME} build ${env.BUILD_NUMBER} failed."
        }
    }
}
