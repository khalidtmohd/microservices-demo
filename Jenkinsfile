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
          sh '''cd /home/ubuntu/microservices-demo
docker login -u mohdkhalid -p Ibrahim@12

skaffold build --default-repo mohdkhalid'''
        }

      }
    }

  }
}