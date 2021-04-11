pipeline {
    agent any
    stages {
        stage('Build') {
            steps{
                sh 'gradlew build'
            }
        }
        stage('Push'){
            steps{
                sh 'docker build --build-arg JAR_FILE=build/libs/\*.jar -t demo .'
            }
        }
    }
}