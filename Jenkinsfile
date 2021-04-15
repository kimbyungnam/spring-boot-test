#!groovy

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
                sh """
                chmod +x gradlew
                ./gradlew build
                pwd
                """

                script{
                    echo "test branch"
                    app = docker.build("demo:$BUILD_NUMBER")
                }
            }
        }
        stage('GitOps'){
            steps{
                script{
                    sh """
                    pwd
                    echo test >> test.yaml
                    git add .
                    git commit -m "test.yaml $BUILD_NUMBER"
                    git push https://$GITOPS_TEST_URL
                    """
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