pipeline {
  agent any
  stages {
    stage('BUZZ Build') {
      parallel {
        stage('Build 7') {
          agent {
            node {
              label 'java7'
            }

          }
          steps {
            sh '''echo "I am ${BUZZ_NAME}"
    sudo    yum install maven -y 
./build.sh
 sudo yum remove maven -y '''
          }
          post {
            always {
            archiveArtifacts(artifacts: 'src/my-app/target/*.jar', fingerprint: true)
            }
            success {
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
          agent {
            node {
              label 'java7'
            }

          }
          steps {
            junit 'src/my-app/target/surefire-reports/**/*.xml'
            unstash 'Buzz Java 7'
          }
        }

        stage('Testing B') {
          agent {
            node {
              label 'java8'
            }

          }
          steps {
            sh '''sleep 10
echo done'''
            unstash 'Buzz Java 8'
          }
        }

      }
    }

    stage('Confirm Deploy') {
      steps {
        input(message: 'Deploy the stage', ok: 'Lets do it', submitter: 'Amjad')
      }
    }

    stage('Deployment') {
      agent {
        node {
          label 'java8'
        }

      }
      steps {
        unstash 'Buzz Java 8'
        sh '''host=$(hostname)
echo $host
echo "I am deployed on $host "'''
      }
    }

  }
  environment {
    BUZZ_NAME = 'WORKER BEE'
  }
}
}
