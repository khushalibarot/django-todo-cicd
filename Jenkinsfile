pipeline{
  agent {label "dev-server"}
  stages{
    stage("code"){
      steps{
        echo "get code from github"
        git url: "https://github.com/khushalibarot/django-todo-cicd.git", branch: "develop"
      }
    }
    stage("build & test"){
      steps{
        echo "build the docker image using docker file"
        sh "docker build -t django-app-new1:latest ."
      }
    }
    stage("push"){
      steps{
       withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerHubPass')]) {
        sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
        sh "docker tag django-app-new1:latest ${env.dockerHubUser}/django-app-new1:latest"
        sh "docker push ${env.dockerHubUser}/django-app-new1:latest"
        sh "echo push the image in docker hub"
        }  
      }
    }
    stage("deploy"){
      steps{
        echo "using docker compose create container and run your application"
        sh "docker-compose down"
        sh "docker-compose up -d"
      }
    }
  }
}
