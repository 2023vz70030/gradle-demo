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
    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }
    steps {
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
