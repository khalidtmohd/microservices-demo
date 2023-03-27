pipeline {
  agent any
  stages {
    stage('BuildStart') {
      steps {
        echo 'Start build'
      }
    }

    stage('fsd') {
      steps {
        grypeScan(scanDest: 'docker:mohdkhalid/php-apache:latest', repName: 'myScanResult.txt', autoInstall: true)
      }
    }

  }
}