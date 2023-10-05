pipeline {
    agent any
    
    stages{
        stage("Clone Code"){
            steps{
                echo "Cloning the Code"
                git url: "https://github.com/MMuzammil6880/Django_Notes_App.git" , branch: "main"
            }
        }
        stage("Build"){
            steps{
                echo "Building the Code"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps{
                echo "Pushing the image into the docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass" ,usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:update1"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:update1"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
