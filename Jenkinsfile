def ingressConfig = "ingress.yaml"

pipeline {
  agent any
  stages {
    stage('Apply ingress') {
      when { branch 'master' }
      steps {
        sh("kubectl apply -f $ingressConfig")
      }
    } 
  }
}
