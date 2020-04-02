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
        script {
            def causes = currentBuild.getBuildCauses()
            causes.each {
                if (it._class == "hudson.model.Cause$UpstreamCause") {
                    echo "Triggered by upstream build!"
                }
            }
        }
        echo "${currentBuild.buildCauses}"
      }
    }
  }

}
