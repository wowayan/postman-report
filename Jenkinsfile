def newmanImage = "postman/newman:latest"

pipeline {
  agent none
  stages {
    stage('Postman-report') {
      agent {
        docker {
          image "${newmanImage}"
          args '--entrypoint='
        }
      }
      steps {
        checkout scm
        script {
          try {
            sh "newman run security/Security-postman_collection.json"
          } catch (err) {
            error "Caught: ${err}"
            currentBuild.result = 'FAILURE'
          }
        }
      }
    }
  }
}
