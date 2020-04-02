pipeline {
  agent {
    node {
      label 'master'
    }
  }

  libraries {
    lib('psikon-jenkins-aptly@master')
  }

  stages {
    stage('Publish') {
      steps {
        echo "${currentBuild.buildCauses}"
      }
    }
  }

}
