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
  -Dsonar.projectKey=MSdemo \\
  -Dsonar.sources=. \\
  -Dsonar.exclusions=src/adservice/src/main/java/hipstershop/** \\
  -Dsonar.host.url=http://65.2.56.210:9000 \\
  -Dsonar.token=sqp_592396504998fe800e2efda080a9875a5a759c6f'''
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
            sh '''#!/bin/bash
echo \'export GOPATH=$HOME/go\' >> ~/.profile
echo \'export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin\' >> ~/.profile
source ~/.profile
for SERVICE in "shippingservice" "productcatalogservice"; do
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