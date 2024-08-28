pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                bat 'mvn clean install'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                bat 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                bat 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                bat 'dependency-check.sh'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                bat 'deploy.sh staging'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                bat 'mvn verify -Pstaging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                bat 'deploy.sh production'
            }
        }
    }
    
    post {
        always {
            echo 'Sending notification emails...'
            mail to: 'IrfanBoenardi1@gmail.com',
                 subject: "Jenkins Pipeline Project by Irfan Boenardi",
                 body: "The project is a success!"
        }
    }
}
