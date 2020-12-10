pipeline {

  environment {
    registry = "lindison/myweb"
    registryCredential = 'dockerhub_id'
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/lindison/test_jenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Cleaning up') {
      steps {
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "$WORKSPACE/hellowhale.yaml", kubeconfigId: "jenkinskubefile")
        }
      }
    }

  }

}
