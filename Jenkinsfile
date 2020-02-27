pipeline {
  agent any
  stages {
    stage('before_install') {
      steps {
        script {
          docker.build("bhavik0907/react-test", "-f ./client/Dockerfile.dev ./client")
        }

      }
    }

    stage('scripts') {
      steps {
        script {
          docker.image('bhavik0907/react-test').withRun('--name react-test -e CI=true') {
            sh 'docker exec react-test npm test'
          }
        }

      }
    }

    stage('after_success') {
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