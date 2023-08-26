pipeline {
    agent any
        stages{
        stage("Git Clone"){
            steps{
                git url: "https://github.com/akashmendhe/calculategrowth.git", branch: "main"
            }
        }
        stage("Create Docker Image"){
            steps{
		    echo "Build and Test"
		    withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "sudo docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "sudo docker build -t kshitibartakke/calculategrowth ."
					}
            }
        }
         stage("Push DockerImage to DockrHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "sudo docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "sudo docker images"
		    sh "sudo docker push akashm123/calculategrowth:latest"
				}
			}
		}
        stage("Deploy Using DOcker Compose"){
            steps{   
		    sh "sudo docker-compose down && docker-compose up -d"           
                }
            }
        }
    }
