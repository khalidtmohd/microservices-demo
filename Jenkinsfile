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
        grypeScan(scanDest: 'repository:mohdkhalid/php-apache:latest', repName: 'myScanResult.txt', autoInstall: true)
      }
    }

  }
}