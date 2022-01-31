pipeline {

  environment {
          AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
          AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
          datadog_apiKey = credentials('datadog_apiKey')
      }

  agent any

  stages {
    
    stage('hello world') {
      steps {
          sh 'echo "Hello World"'
      }
    }

    stage('Helm deploy Datadog') {
      steps {
          withCredentials([file(credentialsId: 'mykubeconfig', variable: 'KUBECONFIG')]) {
            sh 'helm repo add datadog https://helm.datadoghq.com'
            sh 'helm repo update'
        }
      }
    }

  }
}