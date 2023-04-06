pipeline {
  agent none
  stages {
    stage('build') {
      parallel {
        stage('linux-armv6') {
          agent {label 'linux-armv6'}
          steps {
            sh 'go install dpctl'
          }
        }
  
      }
    }
      stage('rollback') {
      steps {
        sh 'git checkout rollback-branch'
        sh 'git revert HEAD'
        sh 'git push origin rollback-branch'
        // deploy rollback changes to production environment
      }
    }
  }
}
