pipeline {
    agent { label 'K8Master-JSlave' }
    //agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials("ef00d982-7b93-437c-a91d-0901156d774c")
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('GitHub-Files') {
            steps {
                script {
                    git 'https://github.com/alps1313/website.git'
                }
            }
        }
        stage('Docker-Image-Push') {
            steps {
                script {
                    sh 'sudo docker build /home/ubuntu/jenkins/workspace/Project2-job/ -t callalps/sampleproject2'
                    sh 'sudo docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}'
                    sh 'sudo docker push callalps/sampleproject2'
                }
            }
        }
        stage('K8s-Deployment-Service') {
            steps {
                sh 'kubectl apply -f deploy.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
