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
                if (it._class == 'hudson.model.Cause$UpstreamCause') {
                    def projectName = it.upstreamProject;
                    def buildNumber = it.upstreamBuild;
                    echo "Triggered by ${projectName}:${buildNumber}"

                    def params = Jenkins.instance.getAllItems(Job);
                } else {
                    echo "Not triggered by upstream build. We can ignore"
                }
            }
        }
        echo "${currentBuild.buildCauses}"
      }
    }
  }

}
