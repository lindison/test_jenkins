pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/lindison/test_jenkins.git', branch:'main'
      }
    }
    
    stage('Deploy App') {
      steps {
        script {
          sh "/usr/local/bin/kubectl apply -f $WORKSPACE/kubernetes-manifests.yaml"
        }
      }
    }

  }

}