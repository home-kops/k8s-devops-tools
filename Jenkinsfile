pipeline {
  agent {
    kubernetes {
      inheritFrom 'agent-s'
    }
  }
  stages {
    stage('Clone') {
      steps {
        git branch: 'main',
          credentialsId: 'github-home-kops-token',
          url: 'https://github.com/home-kops/k8s-devops-tools.git'
      }
    }

    stage('Verify') {
      steps {
        container('jnlp') {
          sh 'kubectl kustomize ./argocd --enable-helm'
          sh 'kubectl kustomize ./jenkins --enable-helm'
          sh 'kubectl kustomize ./renovate --enable-helm'
        }
      }
    }
  }
}
