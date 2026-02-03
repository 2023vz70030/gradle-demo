pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew clean build'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                // Change 'SonarQube' to match the Name in Manage Jenkins > System
                withSonarQubeEnv('SonarQube') { 
                    sh './gradlew sonar'
                }
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }
}
