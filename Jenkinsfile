pipeline {
  /* any means we allow to use any available node to run it */
  agent any

  tools {
    maven 'localMaven'
  }
  
  stages {
    /* stage can have one or more steps */
    stage('Build') {
      /* agent section can also go here*/
      steps {
        sh 'mvn clean package'
      }
      post {
        success {
          echo 'Now archiving'
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }
  }
}
