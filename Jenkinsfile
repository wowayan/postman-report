def collectionName = "security/Security-postman_collection.json"

pipeline {
  agent none
stages {
    stage ("Postman Report") {
          agent {
            docker {
              image "postman/newman:latest"
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
