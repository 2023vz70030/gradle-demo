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
            sh './gradlew clean test'
        }
    }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                    gradle sonarqube \
                    -Dsonar.projectKey=gradle-demo \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.login=<SONAR_TOKEN>
                    '''
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
