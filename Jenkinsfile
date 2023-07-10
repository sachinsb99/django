pipeline{
    agent any
    stages{
        stage("clone code"){
            steps{
                echo "cloning"
                git url:"https://github.com/sachinsb99/django.git", branch: "main"
            }
        }
        
        
             stage("build"){
            steps{
                echo "building"
                sh "docker build -t note-app ."
            }
        }
        
             stage("push"){
            steps{
                echo "pushing docker image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
               sh "docker tag note-app ${env.dockerHubUser}/note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/note-app:latest"
                }
            }
        }
        
             stage("deploy"){
            steps{
                echo "deploying"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
    }   
