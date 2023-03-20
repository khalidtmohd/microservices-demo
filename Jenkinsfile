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
  -Dsonar.sources=. \\
  -Dsonar.host.url=http://43.205.109.218:9000 \\
  -Dsonar.login=sqp_7685e8148b132f66dc0897dbe5b7a55b7b102f3f'''
      }
    }

  }
}