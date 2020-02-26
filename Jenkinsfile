pipeline {
  agent any
  stages {
    stage('before_install') {
      steps {
        bash 'docker build -t bhavik0907/react-test -f ./client/Dockerfile.dev ./client'
      }
    }

    stage('script') {
      steps {
        bash 'docker run -e CI=true --name "react-test" bhavik0907/react-test npm test -- --coverage'
      }
    }

    stage('after_success') {
      steps {
        bash 'docker build -t bhavik0907/multi-client ./client'
        bash 'docker build -t bhavik0907/multi-nginx ./nginx'
        bash 'docker build -t bhavik0907/multi-server./server'
        bash 'docker build -t bhavik0907/multi-worker ./worker'
      }
    }

  }
}
