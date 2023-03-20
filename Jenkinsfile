pipeline {
  agent any
  stages {
    stage('BuildStart') {
      steps {
        echo 'Start build'
      }
    }

    stage('Sonarqube') {
      steps {
        sh '''export PATH="$PATH:/opt/sonar-scanner/bin"
env | grep PATH
sonar-scanner -v
sonar-scanner \\
  -Dsonar.projectKey=test \\
  -Dsonar.sources=src/adservice/src/main/ \\
  -Dsonar.host.url=http://43.205.109.218:9000 \\
  -Dsonar.exclusions=src/adservice/src/main/java/hipstershop/*  \\
  -Dsonar.login=sqp_8bc212bf4a991ff638014a5fb74a79130abb7c1e
'''
      }
    }

  }
}