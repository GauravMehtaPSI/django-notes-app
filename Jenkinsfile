pipeline {
    agent any
    stages {
        stage("Clone the Code") {
            steps {
                echo "cloning the code"
                git url:"https://github.com/GauravMehtaPSI/django-notes-app.git" , branch: "main"
            }
        }
        stage("Build") {
            steps {
                echo "building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Push to DockerHub") {
            steps {
                echo "pushing to dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                
                    
                }
            }
        }
        stage("Deploy") {
            steps {
                echo "deploying the container"
                // sh "docker run -d -p 8000:8000 mehta7/my-note-app:latest"
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }
    
}
