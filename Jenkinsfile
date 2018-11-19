pipeline {
  /* any means we allow to use any available node to run it */
  agent any
  stages {
    /* stage can have one or more steps */
    stage('Build') {
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
    stage('Deploy To Staging') {
      /* agent section can also go here*/
      steps {

      }
    }
  }
}