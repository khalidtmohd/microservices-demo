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

syft packages mohdkhalid/msdemo:adservice --scope all-layers -o json  > sbom-12.json'''
        sh '''grype docker:mohdkhalid/msdemo:adservice -o json > vulns-12.json
          // output vulns as json
         // sh \'grype -o json sbom:sbom-12.json > vulns-12.json\''''
      }
    }

  }
  environment {
    BUILD_NUMBER = '12'
  }
}