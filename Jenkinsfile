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
 -Dsonar.qualitygate.wait=true \\
  -Dsonar.token=sqp_592396504998fe800e2efda080a9875a5a759c6f'''
      }
    }

    stage('unit test') {
      parallel {
        stage('unit test') {
          steps {
            sh '''pwd

docker login -u mohdkhalid -p dckr_pat_K1C6BUyQ5rwcOxmHtiYAOa_wryo


syft packages mohdkhalid/msdemo:adservice --scope all-layers -o json  > sbom-12.json


syft packages dir:./ --scope all-layers -o json  > sbom-msdemo.json

mv filename /home/ubuntu
grype sbom:/home/ubuntu/sbom-msdemo.json

'''
          }
        }

        stage('sds') {
          steps {
            sh '''pwd
mv filename /home/ubuntu
grype sbom:/home/ubuntu/sbom-msdemo.json'''
          }
        }

      }
    }

    stage('error') {
      steps {
        node(label: 'test12') {
          sh 'pwd'
        }

      }
    }

  }
}