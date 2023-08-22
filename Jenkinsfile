node {
  try {
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
    stage('Clean Docker test'){
      sh 'docker rmi react-test'
    }
    stage('Build'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t online-shop-web--no-cache .'
      }
    }
    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker tag online-shop-web localhost:5000/online-shop-web'
        sh 'docker push localhost:5000/online-shop-web'
      }
    }
  }
  catch (err) {
    throw err
  }
}