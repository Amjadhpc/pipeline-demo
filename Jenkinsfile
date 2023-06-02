pipeline {
  agent any
  stages {
    stage('BUZZ Build') {
      steps {
        sh './build.sh'
        archiveArtifacts(artifacts: 'taeget/*.jar', fingerprint: true)
      }
    }

  }
}