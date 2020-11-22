pipeline{    
    agent { label "master" }
    environment {
        ECR_REGISTRY = "089319708029.dkr.ecr.us-east-1.amazonaws.com"
        APP_REPO_NAME= "E2011Yahya/Jenkins-PhonebookApp-on-DockerSwarm"
    }
    stage('Build Docker Image') {

        steps {
            sh 'docker build --force-rm -t "$ECR_REGISTRY/$APP_REPO_NAME:latest" .'
            sh 'docker image ls'
        }
    }
    stage('Push Image to ECR Repo') {

        steps {
            sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin "$ECR_REGISTRY"'
            sh 'docker push "$ECR_REGISTRY/$APP_REPO_NAME:latest"'
        }
    }
    stage('Build the infrastructure'){

        steps{
            sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 089319708029.dkr.ecr.us-east-1.amazonaws.com"
            sh "xxxxxxxxxxxxxxxx"
        }
    }
    stage('Deploy') {
        steps {
            sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin "$ECR_REGISTRY"'
            sh 'docker pull "$ECR_REGISTRY/$APP_REPO_NAME:latest"'
            sh 'docker run --name phonebook-app -dp 80:3000 "$ECR_REGISTRY/$APP_REPO_NAME:latest"'
            }
        }
}
