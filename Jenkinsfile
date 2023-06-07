pipeline {
  agent any
  stages {
    stage('BUZZ Build') {
      parallel {
        stage('Build 7') {
          steps {
            sh '''echo "I am ${BUZZ_NAME}"
        yum install maven -y 
./build.sh
 yum remove maven -y '''
            archiveArtifacts(artifacts: 'src/my-app/target/*.jar', fingerprint: true)
          }
        }

        stage('Build 8') {
          agent {
            node {
              label 'java8'
            }

          }
          steps {
            sh '''echo "I am ${BUZZ_NAME}"
        yum install maven -y 
./build.sh
 yum remove maven -y '''
            archiveArtifacts(artifacts: 'src/my-app/target/*.jar', fingerprint: true)
          }
        }

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