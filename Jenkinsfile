pipeline {
  agent any
  stages {
    stage('BUZZ Build') {
      parallel {
        stage('Build 7') {
          steps {
            sh '''echo "I am ${BUZZ_NAME}"
    sudo    yum install maven -y 
./build.sh
 sudo yum remove maven -y '''
            archiveArtifacts(artifacts: 'src/my-app/target/*.jar', fingerprint: true)
            stash(name: 'Buzz Java 7', includes: 'src/my-app/target/**')
          }
        }

        stage('Build 8') {
          agent {
            node {
              label 'java8'
            }

          }
          environment {
            BUZZ_NAME = 'JAva 8 Bee'
          }
          steps {
            sh '''echo "I am ${BUZZ_NAME}"
     sudo   yum install maven -y 
./build.sh
sudo yum remove maven -y '''
            archiveArtifacts(artifacts: 'src/my-app/target/*.jar', fingerprint: true)
            stash(name: 'Buzz Java 8', includes: 'src/my-app/target/**')
          }
        }

      }
    }

    stage('Buzz Test') {
      parallel {
        stage('Testing A') {
          steps {
            junit 'src/my-app/target/surefire-reports/**/*.xml'
            unstash 'Buzz Java 7'
          }
        }

        stage('Testing B') {
          steps {
            sh '''sleep 10
echo done'''
            unstash 'Buzz Java 8'
          }
        }

      }
    }

  }
  environment {
    BUZZ_NAME = 'WORKER BEE'
  }
}