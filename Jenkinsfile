pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/lindison/test_jenkins', branch:'main'
      }
    }
    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "kubernetes-manifests.yaml", kubeconfigId: "jenkinskubefile")
        }
      }
    }

  }

}