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
        sh './gradlew clean test'
    }
}

    stage('SonarQube Analysis') {
    steps {
        withSonarQubeEnv('SonarQube') {
            sh 'chmod +x gradlew'
            sh './gradlew sonarqube'
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
