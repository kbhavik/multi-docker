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
          clientimg = docker.build("bhavik0907/multi-client", "./client")
          nginximg = docker.build("bhavik0907/multi-nginx", "./nginx")
          serverimg = docker.build("bhavik0907/multi-server", "./server")
          workerimg = docker.build("bhavik0907/multi-worker", "./worker")
        }
      }
    }

    stage('push_images') {
      steps {
        docker.withRegistry('https://index.docker.io/v1/', 'Docker-hub') {
        //withDockerRegistry([ credentialsId: "Docker-hub", url: "https://index.docker.io/v1/" ]) {
          // sh 'docker push bhavik0907/multi-client'
          // sh 'docker push bhavik0907/multi-nginx'
          // sh 'docker push bhavik0907/multi-server'
          // sh 'docker push bhavik0907/multi-worker'
          clientimg.push()
          nginximg.push()
          serverimg.push()
          workerimg.push()
        }
      }
    }
  }
}