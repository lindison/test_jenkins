pipeline {
  agent {
    docker { image 'node:14-alpine'}
  }

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
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "jenkinskubefile")
        }
      }
    }

  }

}
