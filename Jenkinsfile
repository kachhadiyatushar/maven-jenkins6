pipeline {
    agent any
    stages {
        stage('git-code-download') {
            steps {
                echo "Download code from Git"
                git branch: 'main', url: 'https://github.com/kachhadiyatushar/maven-jenkins6.git'
            }
        }
        stage('create-docker-image') {
            steps {
                sh '''
                docker build -t kachhadiyatushar/javawebapp:${BUILD_NUMBER} .
                docker tag kachhadiyatushar/javawebapp:${BUILD_NUMBER} kachhadiyatushar/javawebapp:latest
                docker push kachhadiyatushar/javawebapp:${BUILD_NUMBER}
                docker push kachhadiyatushar/javawebapp:latest
                '''
            }
        }
        stage('deploy') {
            steps {
                build 'docker-deploy'
            }
        }
    }
}
