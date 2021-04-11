pipeline {
    agent any
    stages {
        stage('Clone repository'){
            checkout scm
        }
        stage('Build') {
            app = docker.build("demo:$BUILD_NUMBER")
        }
        stage('Push'){
            steps{
                docker.withRegistry("https://harbor.gaonna.tech", "jenkins_test")
                app.push("$BUILD_NUMBER")
            }
        }
    }
}