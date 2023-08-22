pipeline {
  agent any
    stages {
      stage('Checkout') {
        checkout scm
      }
      stage('Environment') {
        steps {
          sh 'git --version'
          echo "Branch: ${env.BRANCH_NAME}"
          sh 'docker -v'
          sh 'printenv'
        }
      }

      stage('Docker test'){
        sh 'docker run --rm react-test'
      }

      stage('Build') {
        steps {
          script {
            if(env.BRANCH_NAME == 'master'){
              sh 'docker build -t online-shop-web .'
            }
          }
        }
      }

      stage('Deploy') {
        steps {
          script {
            if(env.BRANCH_NAME == 'master'){
              sh 'docker push online-shop-web'
            }
          }
        }
      }
    }

}