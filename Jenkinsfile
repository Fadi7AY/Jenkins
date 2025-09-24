pipeline {
  agent {
    docker {
      image 'docker:27-cli'                 // has docker CLI
      args '-v /var/run/docker.sock:/var/run/docker.sock'
      reuseNode true
    }
  }

  environment {
    IMAGE_NAME = "fadi7ay/fadi_jenkins_docker22:${env.BUILD_NUMBER}"
  }

  stages {
    stage('Check Docker') {
      steps {
        sh 'docker version'
      }
    }

    stage('Build Image') {
      steps {
        sh 'docker build -t $IMAGE_NAME .'
      }
    }

    stage('Login & Push') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'dockerhub',
          usernameVariable: 'DOCKERHUB_USER',
          passwordVariable: 'DOCKERHUB_PASS'
        )]) {
          sh '''
            echo "$DOCKERHUB_PASS" | docker login -u "$DOCKERHUB_USER" --password-stdin
            docker push "$IMAGE_NAME"
            docker logout || true
          '''
        }
      }
    }
  }
}
