pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm // Pulls code from GitHub
            }
        }

 	stage('Set Gradle Wrapper Executable') {
            steps {
                sh 'chmod +x gradlew'
            }
        }
        stage('Build & Test') {
            steps {
                sh './gradlew clean test' // Runs Gradle build
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true // Saves the JAR
            }
        }
    }
}
