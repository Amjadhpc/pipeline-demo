pipeline {
  agent any
  stages {
    stage('BUZZ Build') {
      steps {
        sh '''echo I am $BUZZ_NAME
./build.sh'''
        archiveArtifacts(artifacts: 'src/my-app/target/*.jar', fingerprint: true)
      }
    }

    stage('Buzz Test') {
      steps {
        junit 'src/my-app/target/surefire-reports/**/*.xml'
      }
    }

  }
  environment {
    BUZZ_NAME = 'WORKER BEE'
  }
}