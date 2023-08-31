pipeline {

  environment {
    dockerimagename = "naveen047/react-app"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
<<<<<<< HEAD
        git 'https://github.com/NSR270495/React-App.git'
=======
        git url:'https://github.com/NSR270495/React-App.git', branch:'main'
>>>>>>> 1480e9787d3005c239b59d7dab1104e2b78218b2
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhub-credentials'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        }
      }
    }

  }

}
