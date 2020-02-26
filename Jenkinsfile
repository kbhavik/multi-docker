pipeline {
  agent any
  stages {
    stage('before_install') {
      agent any
      steps {
        script {
          docker.build("bhavik0907/react-test", "-f ./client/Dockerfile.dev ./client")
        }

      }
    }

    stage('scripts') {
      agent any
      steps {
        script {
          sh 'docker run -e CI=true bhavik0907/react-test npm test'
        }

      }
    }

    stage('after_success') {
      agent any
      steps {
        script {
          sh 'docker build -t bhavik0907/multi-client ./client'
          sh 'docker build -t bhavik0907/multi-nginx ./nginx'
          sh 'docker build -t bhavik0907/multi-server./server'
          sh 'docker build -t bhavik0907/multi-worker ./worker'
        }

      }
    }

  }
}