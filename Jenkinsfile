pipeline {
    agent any
    stages {
        stage('Clone repository'){
            steps{
                checkout scm
            }
        }
        stage('Build') {
            steps{
                app = docker.build("demo:$BUILD_NUMBER")
            }
        }
        stage('Push'){
            steps{
                docker.withRegistry("https://harbor.gaonna.tech", "jenkins_test")
                app.push("$BUILD_NUMBER")
            }
        }
    }
}