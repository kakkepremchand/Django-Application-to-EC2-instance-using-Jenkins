pipeline {
    agent any 
    
    stages{
        stage("CLONING THE CODE"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/premchandkakke/django-notes-app.git", branch: "main"
            }
        }
        stage("BUILDING THE IMAGE"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("PUSH TO THE DOCKER HUB"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId: 'docker Hub', passwordVariable: 'dockerPass', usernameVariable: 'dockerVar')]) {
                sh "docker tag my-note-app ${env.dockerVar}/my-note-app:latestnew"
                sh "docker login -u ${env.dockerVar} -p ${env.dockerPass}"
                sh "docker push ${env.dockerVar}/my-note-app:latestnew"
                }
            }
        }
        stage("DEPLOYING THE CONTAINER"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
