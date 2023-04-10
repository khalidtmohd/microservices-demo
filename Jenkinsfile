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

    stage('Skaffold Build') {
      steps {
        node(label: 'test12') {
          sh '''pwd
docker login -u mohdkhalid -p dckr_pat_K1C6BUyQ5rwcOxmHtiYAOa_wryo

skaffold build --default-repo docker.io/mohdkhalid'''
        }

      }
    }

    stage('Syft Sbom') {
      steps {
        sh '''docker login -u mohdkhalid -p dckr_pat_K1C6BUyQ5rwcOxmHtiYAOa_wryo


syft packages mohdkhalid/adservice:86511cf  -o json  > adservice.json

syft packages mohdkhalid/currencyservice:86511cf  -o json  > currencyservice.json
syft packages mohdkhalid/shippingservice:86511cf  -o json  > shippingservice.json
syft packages mohdkhalid/frontend:86511cf  -o json  > frontend.json
syft packages mohdkhalid/paymentservice:86511cf  -o json  > paymentservice.json
syft packages mohdkhalid/cartservice:86511cf  -o json  > cartservice.json
syft packages mohdkhalid/recommendationservice:86511cf  -o json  > recommendationservice.json
syft packages mohdkhalid/productcatalogservice:86511cf  -o json  > productcatalogservice.json
syft packages mohdkhalid/emailservice:86511cf -o json  > emailservice.json
syft packages mohdkhalid/checkoutservice:86511cf  -o json  > checkoutservice.json
syft packages mohdkhalid/loadgenerator:86511cf  -o json  > loadgenerator.json

syft packages dir:./ --scope all-layers -o json  > sbom-msdemo.json


'''
      }
    }

    stage('Grype Vulnerability') {
      steps {
        sh '''grype sbom:./sbom-msdemo.json -o json > grype-vulnerability.json

grype sbom:./adservice.json -o json > adservicevulnerability.json 
grype sbom:./currencyservice.json -o json > currencyservicevulnerability.json 
grype sbom:./shippingservice.json -o json > shippingservicevulnerability.json
grype sbom:./frontend.json -o json > frontendvulnerability.json
grype sbom:./paymentservice.json -o json > paymentservicevulnerability.json
grype sbom:./cartservice.json -o json > cartservicevulnerability.json
grype sbom:./recommendationservice.json -o json > recommendationservicevulnerability.json
grype sbom:./productcatalogservice.json -o json > productcatalogservicevulnerability.json
grype sbom:./emailservice.json -o json > emailservicevulnerability.json
grype sbom:./checkoutservice.json -o json > checkoutservicevulnerability.json
grype sbom:./loadgenerator.json -o json > loadgeneratorvulnerability.json
'''
      }
    }

    stage('Archive') {
      parallel {
        stage('Archive') {
          steps {
            archiveArtifacts '*.json'
          }
        }

        stage('Deploy') {
          steps {
            node(label: 'test12') {
              sh '''docker login -u mohdkhalid -p dckr_pat_K1C6BUyQ5rwcOxmHtiYAOa_wryo

skaffold run --default-repo docker.io/mohdkhalid'''
            }

          }
        }

      }
    }

  }
}