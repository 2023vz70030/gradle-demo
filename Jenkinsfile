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
        withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
            withSonarQubeEnv('SonarQube') {
                sh """
                chmod +x gradlew
                ./gradlew sonar \
                  -Dsonar.login=$SONAR_TOKEN
                """
            }
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
