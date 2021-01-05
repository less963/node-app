pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t less963/nodeapp:${DOCKER_TAG}"
            }
        }
        stage('DockerHub Push'){
           steps{
                withCredentials([string(credentialsId: 'less963', variable: 'dockerHubPwd')]) {
            sh "docker login -u less963 -p ${dockerHubPwd}"
            sh "docker push less963/nodeapp:${DOCKER_TAG}"
            }
           }
        }
    }
}

def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}