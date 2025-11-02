@Library("Shared") _

pipeline {
    agent { label 'agent-sardar' }

    stages {
        stage('Hello'){
            steps{
                script{
                    hello()
                }
            }
        }
        stage('Code') {
            steps {
                script{
                    repoClone('main','https://github.com/firojbabu452/django-notes-app.git')
                }
            }
        }

        stage('Build') {
            steps {
                script{
                    docker_build('notes-app','latest','firojbabu452')
                }
            }
        }

       stage('Push To Docker Hub') {
            steps {
               docker_push("notes-app","latest","firojbabu452")
    }
       }

        stage('Deploy') {
            steps {
                echo 'Deploying the code'
                sh "docker compose down || true"
                sh "docker compose up -d"
            }
        }
    }
}
