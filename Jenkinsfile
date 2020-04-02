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
                println it
            }
        }
/*
        def parameters = Jenkins.instance.getAllItems(Job)
                        .find {job -> job.fullName == jobName }
                        .getBuildByNumber(buildId.toInteger())
*/
        echo "${currentBuild.buildCauses}"
      }
    }
  }

}
