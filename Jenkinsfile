pipeline {
  agent any
  stages {
    stage('Fluffy Build') {
      steps {
        echo 'Build'
        sh 'echo Edited Placeholder.'
         sudo   yum install maven -y 
./build.sh
sudo yum remove maven -y '''
            archiveArtifacts(artifacts: 'src/my-app/target/*.jar', fingerprint: true)
      }
    }
    stage('Fluffy Test') {
      parallel {
        stage('Backend') {
          steps {
            sh 'echo backend'
            junit 'src/my-app/target/surefire-reports/**/TEST*.xml'
          }
        }
        stage('Frontend') {
          steps {
            sh 'echo frontend'
            junit '/src/my-app/target/test-results/**/TEST*.xml'
          }
        }
        stage('Performance') {
          steps {
            sh 'echo performance'
          }
        }
        stage('Static') {
          steps {
            sh 'echo static'
          }
        }
      }
    }
    stage('Fluffy Deploy') {
      steps {
        sh 'echo deploy'
      }
    }
  }
}
