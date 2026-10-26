pipeline {
    agent any

    environment {
         CONTAINER_NAME = "nestjs-app"
         IMAGE_NAME = "nestjs-image"
         EMAIL = "abdullah.sysconinfotech@gmail.com"
         PORT = "3000"
    }

    stages{
        stage("Clone Repo"){
            steps {
                git branch: "main", url : "https://github.com/abdullah-sysconinfotech/CI-CD-Jenkins-Docker-AWS-GithubWebhook.git"
            }
        }

        stage("Build Docker Image"){
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage("Stop & Remove Previous Container"){
            steps {
                sh '''
                 docker stop $CONTAINER_NAME || true
                 docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage("Docker Container Run"){
            steps {
                sh '''
                 docker run -d -p ${PORT}:${PORT} $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage("Send Email & Notification"){
            steps {
                emaillext(
                    subject : "NestJs Deployed Successfully on EC2",
                    body : "Your NestJs App is Deployed! http://3.110.76.102:${PORT}/",
                    to: "${EMAIL}"
                )
            }
        }
    }
}