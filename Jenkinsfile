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
          def clientImg = docker.build("bhavik0907/multi-client", "./client")
          def nginxImg = docker.build("bhavik0907/multi-nginx", "./nginx")
          def serverImg = docker.build("bhavik0907/multi-server", "./server")
          def workerImg = docker.build("bhavik0907/multi-worker", "./worker")
        }

      }
    }

    stage('push_images') {
      steps {
        sh '''docker.withRegistry(\'https://hub.docker.com/\', \'Docker-hub\') {
clientImg.push()
nginxImg.push()
serverImg.push()
workerImg.push()
}'''
        }
      }

    }
  }