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
        bat(script: 'react-test.bat', returnStdout: true, returnStatus: true)
      }
    }

    stage('after_success') {
      steps {
        script {
          docker.build("bhavik0907/multi-client", "./client")
          docker.build("bhavik0907/multi-nginx", "./nginx")
          docker.build("bhavik0907/multi-server", "./server")
          docker.build("bhavik0907/multi-worker", "./worker")
        }

      }
    }

    stage('push_images') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'Docker-hub') {
            'bhavik0907/multi-client'.push()
            'bhavik0907/multi-nginx'.push()
            'bhavik0907/multi-server'.push()
            'bhavik0907/multi-worker'.push()
          }
        }

      }
    }

  }
}