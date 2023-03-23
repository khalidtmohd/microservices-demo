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
  -Dsonar.sources=.  \\
  -Dsonar.host.url=http://65.1.145.233:9000 \\
  -Dsonar.exclusions=src/adservice/src/main/java/hipstershop/*  \\
  -Dsonar.login=sqp_8bc212bf4a991ff638014a5fb74a79130abb7c1e
'''
      }
    }

    stage('unit test') {
      parallel {
        stage('unit test') {
          steps {
            sh 'dotnet test src/cartservice/'
          }
        }

        stage('go unit test') {
          steps {
            sh '''for SERVICE in "shippingservice" "productcatalogservice"; do
          echo "testing $SERVICE..."
          pushd src/$SERVICE
          go test
          popd
        done'''
          }
        }

      }
    }

  }
}