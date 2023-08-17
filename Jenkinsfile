pipeline {
  agent any
    stages {
      stage('Checkout') {
        steps {
          checkout scm
          }
      }
      stage('Environment') {
        stages {
          sh 'git --version'
          echo "Branch: ${env.BRANCH_NAME}"
          sh 'docker -v'
          sh 'printenv'
        }
      }
      stage('Build Docker test'){
        stages {
          sh 'docker build -t react-test -f Dockerfile.test --no-cache .'
         }
      }
      stage('Docker test'){
        stages {
          sh 'docker run --rm react-test'
        }
      }
      stage('Clean Docker test'){
        stages {
          sh 'docker rmi react-test'
        }
      }
      stage('Deploy'){
        stages {
          if(env.BRANCH_NAME == 'master'){
            sh 'docker build -t online-shop-web--no-cache .'
            sh 'docker tag online-shop-web localhost:5000/online-shop-web'
            sh 'docker push localhost:5000/online-shop-web'
            sh 'docker rmi -f online-shop-web localhost:5000/online-shop-web'
          }
        }
      }
    }
    catch (err) {
      throw err
    }
}