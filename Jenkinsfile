pipeline {
  agent {
    node {
      label 'master'
    }
  }

  libraries {
    lib('pipeline-jenkins-aptly@master')
  }

  stages {
    stage('Publish') {
      steps {
        publishDeb
      }
    }
  }

}
