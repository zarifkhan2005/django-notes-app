@Library("shared") _

pipeline {
    agent any

    stages {

        stage("Hello") {
            steps {
                script {
                    hello()
                }
            }
        }

        stage('Code') {
            steps {
                script {
                    gitClone(
                        "https://github.com/zarifkhan2005/django-notes-app.git",
                        "main"
                    )
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    docker_build(
                        "notes-app",
                        "latest",
                        "zarifkhanjaveed"
                    )
                }
            }
        }

        stage('Test') {
            steps {
                echo 'This is testing the code'
            }
        }

        stage("Push to Docker Hub") {
            steps {
                script {
                    docker_push(
                        "notes-app",
                        "latest",
                        "zarifkhanjaveed"
                    )
                }
            }
        }

        stage('Deploy') {
            steps {

                sh 'docker rm -f notes-app-container || true'
                echo "solve the error"
                sh 'docker run -d -p 8000:8000 --name notes-app-container notes-app:latest'
            }
        }
    }
}
