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
        stage('darwin-amd64') {
          agent {label 'darwin-amd64'}
          steps {
            sh 'go install dpctl'
          }
        }
        stage('linux-amd64') {
          agent {label 'linux-amd64'}
          steps {
            sh 'go install dpctl'
          }
        }
      }
    }
    stage('run') {
      parallel {
        stage('linux-armv6') {
          agent {label 'linux-armv6'}
          steps {
            sh 'dpctl'
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
