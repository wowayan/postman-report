def newmanImage = "postman/newman:latest"

pipeline {
  agent none

  options {
    ansiColor('xterm')
    buildDiscarder(
      logRotator(
        artifactDaysToKeepStr: '',
        artifactNumToKeepStr: '',
        daysToKeepStr: '60',
        numToKeepStr: '50'
      )
    )
    disableConcurrentBuilds()
    timeout(time: 60, unit: 'MINUTES')
    timestamps()
  }

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
