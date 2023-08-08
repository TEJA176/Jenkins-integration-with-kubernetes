pipeline {

  environment {
    dockerimagename = "tejendranadu/nodeapp"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/TEJA176/nodeapp_test.git'
      }
    }

    stage('Build image') {
      steps{
        script {
         // dockerImage = docker.build dockerimagename
          sh 'docker build -t docmyimage .'
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhublogin'
           }
      steps{
        script {
          docker.withRegistry( 'https://hub.docker.com/', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Deploying App to Kubernetes') {
      steps {
        script {
          sh 'kubectl apply -f deploymentservice.yml'
        }
      }
    }

  }

}
