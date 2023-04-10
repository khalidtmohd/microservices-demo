pipeline {
  agent {
    node {
      label 'test'
    }

  }
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
            pwd()
          }
        }

      }
    }

    stage('') {
      steps {
        pwd()
      }
    }

  }
}