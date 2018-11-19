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

    stage('Deploy To Staging') {
      steps {
        build job: 'deploy-to-staging'
      }
    }

    stage('Deploy To Production') {
      steps {
        timeout(time:5, unit: 'DAYS') {
          input message: 'Approve PRODUCTION Deployment ?'
        }
        build job: 'deploy-to-prod'
      }
      post {
        success {
          echo 'Code Deployed to Production'
        }
        failure {
          echo 'Deployment failure'
        }
      }
    }
  }
}
