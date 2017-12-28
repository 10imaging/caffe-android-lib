pipeline {
  agent { label 'master' }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
        sh 'git submodule update --init --recursive'
      }
    }
    stage ('Build') {
      steps {
        echo "Branch: ${env.BRANCH_NAME}"
        echo "Build#: ${env.BUILD_NUMBER}"
        echo "ID: ${env.CHANGE_ID}"
        echo "Author: ${env.CHANGE_AUTHOR}"
        environment {
          DEBUG_BUILD = "true"
        }
        sh "rm -rf build"
        sh "./build-all.sh clean"
      }
    }
    stage ('Archive') {
      step([$class: 'ArtifactArchiver', artifacts: 'build/**', fingerprint: true])
    }
  }
}
