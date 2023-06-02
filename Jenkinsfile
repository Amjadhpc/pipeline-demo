pipeline {
  agent any
  stages {
    stage('BUZZ Build') {
      steps {
        sh './build.sh'
        archiveArtifacts(artifacts: 'src/my-apptarget/*.jar', fingerprint: true)
      }
    }

  }
}