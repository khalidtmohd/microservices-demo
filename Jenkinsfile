pipeline {
  agent any
  stages {
    stage('BuildStart') {
      parallel {
        stage('BuildStart') {
          steps {
            echo 'Start build'
          }
        }

        stage('test') {
          steps {
            sh 'grype docker:mohdkhalid/php-apache:latest -o json > grype-vulnerability.json'
            fileExists 'rgrype-vulnerability.json'
          }
        }

      }
    }

    stage('error') {
      steps {
        sh '''cd src/adservice
docker build . -t mohdkhalid/msdemo:adservice
docker login -u mohdkhalid -p Ibrahim@12
docker push mohdkhalid/msdemo:adservice'''
        pwd()
        sh '''docker login -u mohdkhalid -p Ibrahim@12

syft mohdkhalid/msdemo:adservice-o json adservice:${BUILD_NUMBER} > sbom-${BUILD_NUMBER}.jso'''
      }
    }

  }
}