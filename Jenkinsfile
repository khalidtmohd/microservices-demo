pipeline {
  agent any
  stages {
    stage('BuildStart') {
      steps {
        echo 'Start build'
      }
    }

    stage('deploy') {
      steps {
        node(label: 'test') {
          sh '''cd microservicesdemo
skaffold build'''
        }

      }
    }

  }
}