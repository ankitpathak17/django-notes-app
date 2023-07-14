pipeline{
    agent any

    stages{
        stage("Code"){
            steps{
                echo "Cloning code"
                git url: "https://github.com/ankitpathak17/django-notes-app.git", branch: "main"

            }

        }
        stage("Build"){
            steps{
                echo "Building the code"
                sh "docker build -t my-notes-app ."
                
            }

        }
        stage("Push to docker hub"){
            steps{
                echo "pushing to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable: "dockerHubPass",usernameVariable:"dockerHubuser")]){
                sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh " docker push ${env.dockerHubUser}/my-notes-app:latest"
                }
               
            }

        }
        stage("Deploy"){
            steps{
                echo "deploying  code"
                 //sh "docker run d -p 8000:8000 ankitpathak101/my-notes-app:latest "
                 sh "docker-compose down && docker-compose up -d"

            }

        }

    }

}
