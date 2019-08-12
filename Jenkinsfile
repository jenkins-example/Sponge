pipeline {
    agent {
        docker {
            image 'openjdk:8u222-jre-stretch'
            args '--name jenkins-Jenkins_Sponge'
        }
    }
    stages {
        stage('Pre-Build') {
            steps {
                sh 'chmod +x gradlew'
            }
        }
        stage('Build') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
        }
    }
}