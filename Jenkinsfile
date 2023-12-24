pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/yoursmanjunad/DevOps-Project-1.0.0.git", branch: "master"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"Docker",passwordVariable:"DockerPass",usernameVariable:"DockerUser")]){
                sh "docker tag my-note-app ${env.DockerUser}/my-note-app:latest"
                sh "docker login -u ${env.DockerUser} -p ${env.DockerPass}"
                sh "docker push ${env.DockerUser}/my-note-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
