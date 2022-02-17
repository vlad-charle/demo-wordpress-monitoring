pipeline {
  environment {
          // Use AWS credentials saved in Jenkins as secret text and use DataDog API key stored in Jenkins as secret text
          AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
          AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
          datadog_apiKey = credentials('datadog_apiKey')
      }

  agent any

  stages {
    stage('Helm add & update Datadog repo') {
      // Add DataDog Helm repo and update it
      steps {
          withCredentials([file(credentialsId: 'mykubeconfig', variable: 'KUBECONFIG')]) {
            sh 'helm repo add datadog https://helm.datadoghq.com'
            sh 'helm repo update'
        }
      }
    }
    stage('Helm deploy Datadog') {
      // Deploy DataDog to AWS EKS using Helm with kubeconfig, that is stored as secret file credential in Jenkins
      steps {
          withCredentials([file(credentialsId: 'mykubeconfig', variable: 'KUBECONFIG')]) {
                sh '''
                    helm install datadog -f datadog-values.yaml --set datadog.site='datadoghq.com' --set datadog.apiKey=${datadog_apiKey} datadog/datadog
                '''
        }
      }
    }
  }
}