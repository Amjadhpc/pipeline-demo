pipeline {
  agent any
  stages {
    stage('BUZZ Build') {
      steps {
        sh '''echo "I am ${BUZZ_NAME}"
./build.sh'''
        archiveArtifacts(artifacts: 'src/my-app/target/*.jar', fingerprint: true)
      }
    }

    stage('Buzz Test') {
      parallel {
        stage('Testing A') {
          steps {
            junit 'src/my-app/target/surefire-reports/**/*.xml'
          }
        }

        stage('Testing B') {
          steps {
            sh '''sleep 10
echo done'''
          }
        }

      }
    }

  }
  environment {
    BUZZ_NAME = 'WORKER BEE'
  }
}
