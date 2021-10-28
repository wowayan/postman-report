def newmanImage = "dannydainton/htmlextra:latest"

pipeline {
      agent {
        docker {
          image "${newmanImage}"
          args '--entrypoint='
        }
      }
  stages {
    stage('Postman-report') {
      steps {
        checkout scm
        script {
          try {
            sh "newman run security/Security-postman_collection.json -r htmlextra --reporter-htmlextra-export ./postman/report.html "
          } catch (err) {
            error "Caught: ${err}"
            currentBuild.result = 'FAILURE'
          }
        }
      }
    }
  }
}
