pipeline {
  agent {
    node {
      label 'master'
    }
  }

  triggers {
    upstream(upstreamProjects: 'psistats/psistats-rs/master', threshold: hudson.model.Result.SUCCESS)
  }

  libraries {
    lib('psikon-jenkins-aptly@master')
    lib('psikon-jenkins-mailer@master')
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
   
                    copyArtifacts(
                        filter: '**/*.deb', 
                        projectName: projectName, 
                        selector: specific(buildNumber.toString()),
                        flatten: true,
                        target: 'target/artifacts'
                    )

                    def debs = findFiles glob: 'target/artifacts/*.deb'

                    debs.each { deb ->
                        echo "Publishing debian file: $deb"
                        publishDeb component: 'testing', distribution: 'psikon', debFile: deb, repoName: 'psikon-testing'
                    }

                } else {
                    copyArtifacts(
                        filter: '**/*.deb',
                    echo "Not triggered by upstream build. We can ignore"
                }
            }
        }
        echo "${currentBuild.buildCauses}"
      }
    }
  }
  post {
    success {
      psikonMailer(currentBuild, env)
    }

    failure {
      psikonMailer(currentBuild, env)
    }
  }
}
