def newmanImage = "postman/newman:latest"
def collectionName = "security/Security-postman_collection.json"

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
    stage ("Postman Report") {
          agent {
            docker {
              image "${newmanImage}"
              args '-u 0 -v /var/run/docker.sock:/var/run/docker.sock:rw'
            }
          }
          steps {
            checkout scm
            script {
              try {
                sh """
                  newman run '$collectionName'
                """
              } catch (err) {
                error "Caught: ${err}"
                currentBuild.result = 'FAILURE'
              }
            }
          }
        }
  }
}
