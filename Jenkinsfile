pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/NSR270495/React-App.git', branch:'main'
      }
    }

    stage('Build image'){
       steps{
                    withCredentials([usernamePassword(credentialsId: 'Dockerhub-Credential', passwordVariable: 'Password', usernameVariable: 'Username')]) {
           sh "sudo docker build -t naveen047/react-app"
           }
       }
    }

     stage('Pushing Image'){
       steps{
          withCredentials([usernamePassword(credentialsId: 'Dockerhub-Credential', passwordVariable: 'Password', usernameVariable: 'Username')]) {
             sh "sudo docker push naveen047/react-app:latest"
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
