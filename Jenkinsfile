pipeline{
  agent any
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
        sh "docker build -t django-app:latest ."
      }
    }
    stage("push"){
      steps{
        echo "push docker image on dockerhub"
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
