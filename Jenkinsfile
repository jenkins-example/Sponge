def PROJECT_NAME = 'Jenkins_Sponge' // Be aware that PROJECT_NAME cannot contain space, which is not a valid docker container name

pipeline {
    agent {
        docker {
            image 'openjdk:8u222-jdk-stretch'
            args "--name jenkins-${PROJECT_NAME}"
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
            sh 'pwd'
            sh 'ls build/libs/'
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
        }
        always {
            deleteDir()
        }
    }
}