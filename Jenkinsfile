pipeline {
  agent any
  stages {
    stage('BUZZ Build') {
    parallel{
      stage('Build Java 7'){
      steps {
        sh '''echo "I am ${BUZZ_NAME}"
./build.sh'''
}

post {
 always{
        archiveArtifacts(artifacts: 'src/my-app/target/*.jar', fingerprint: true)
 }    
  success {
     stash (name: 'Buzz Java 7',includes : 'src/my-app/target/**')  
  
         }
     }
    }
  
  }
}
}
}
}
