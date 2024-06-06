pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials("1fce6454-30f0-46ea-84c0-fe8dd129a0d0")
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
                    sh 'sudo docker build /home/ubuntu/jenkins/workspace/Pipeline/ -t callalps/sampleproject2'
                    sh 'sudo docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}'
                    sh 'sudo docker push callalps/sampleproject2'
                }
            }
        }
        stage('K8s-Deployment-Service') {
            steps {
                sh 'kubectl delete deploy nginx-deployment'
                sh 'kubectl apply -f deploy.yaml'
                sh 'kubectl delete service my-service'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
