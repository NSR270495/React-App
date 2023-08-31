pipeline {

#  environment {
#    dockerimagename = "naveen047/react-app"
#    dockerImage = ""
#  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/NSR270495/React-App.git', branch:'main'
      }
    }

    stage('Build image'){
       steps{
           sh "sudo docker build -t naveen047/react-app"
       }
    }
#    stage('Build image') {
#      steps{
#        script {
#          dockerImage = docker.build dockerimagename
#        }
#      }
#    }

     stage('Pushing Image'){
       steps{
          withCredentials([usernamePassword(credentialsId: 'Dockerhub-Credential', passwordVariable: 'Password', usernameVariable: 'Username')]) {
             sh "sudo docker push naveen047/react-app:latest"
          }
       }
     }

#    stage('Pushing Image') {
#      environment {
#               registryCredential = 'dockerhub-credentials'
#           }
#      steps{
#        script {
#          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
#            dockerImage.push("latest")
#          }
#        }
#      }
#    }

    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        }
      }
    }

  }

}
