pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/lindison/test_jenkins.git'
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "$WORKSPACE/kubernetes-manifests.yaml", kubeconfigId: "jenkinskubefile")
        }
      }
    }

  }

}
