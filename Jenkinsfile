pipeline {
  agent any
  stages {
    stage('BUZZ Build') {
      steps {
        sh './build.sh'
        archiveArtifacts(artifacts: 'src/my-app/target/*.jar', fingerprint: true)
      }
    }

    stage('Buzz Test') {
      steps {
        junit 'src/my-app//surefire-reports/**/*.xml'
      }
    }

  }
}