pipeline {
  agent any
  stages {
    stage('before_install') {
      steps {
        
        docker.build("bhavik0907/react-test", "-f ./client/Dockerfile.dev ./client")
      }
    }

    stage('script') {
      steps {
        sh 'docker run -e CI=true --name "react-test" bhavik0907/react-test npm test -- --coverage'
      }
    }

    stage('after_success') {
      steps {
        sh 'docker build -t bhavik0907/multi-client ./client'
        sh 'docker build -t bhavik0907/multi-nginx ./nginx'
        sh 'docker build -t bhavik0907/multi-server./server'
        sh 'docker build -t bhavik0907/multi-worker ./worker'
      }
    }

  }
}
