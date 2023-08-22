pipeline {
  agent any
  stages {
    stage('Checkout') {
      checkout scm
    }
    stage('Environment') {
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'docker -v'
      sh 'printenv'
    }
    stage('Docker test'){
      sh 'docker run --rm react-test'
    }
    stage('Build') {
      steps {
        if(env.BRANCH_NAME == 'master'){
          sh 'docker build -t my-app .'
        }
      }
    }

    stage('Deploy') {
      steps {
        if(env.BRANCH_NAME == 'master'){
          sh 'docker push my-app'
        }
      }
    }
  }
  catch (err) {
    throw err
  }
}