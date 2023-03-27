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
        grypeScan(scanDest: 'mohdkhalid/php-apache:latest', repName: 'myScanResult.txt', autoInstall: true)
      }
    }

  }
}