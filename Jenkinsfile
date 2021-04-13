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
                sh './gradlew build'
                script{
                    echo "test branch"
                    app = docker.build("demo:$BUILD_NUMBER")
                }
            }
        }
        stage('Push'){
            steps{
                script{
                    docker.withRegistry("https://harbor.gaonna.tech", "jenkins_test")
                    app.push("$BUILD_NUMBER")
                }
            }
        }
    }
}