pipeline {
  agent any
    stages {
      stage('Checkout') {
        steps {
          checkout scm
        }
      }
      stage('Environment') {
        steps {
          sh 'git --version'
          echo "Branch: ${env.BRANCH_NAME}"
          sh 'docker -v'
          sh 'printenv'
        }
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