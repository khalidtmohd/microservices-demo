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
            sh 'grype mohdkhalid/php-apache:latest -o json > grype-vulnerability.json'
            fileExists 'rgrype-vulnerability.json'
          }
        }

      }
    }

    stage('fsd') {
      steps {
        grypeScan(scanDest: 'mohdkhalid/php-apache:latest', repName: 'myScanResult.txt', autoInstall: true)
      }
    }

  }
}