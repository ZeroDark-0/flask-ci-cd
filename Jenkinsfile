pipeline {
  agent any
  environment {
    IMAGE = 'zerodark0/flask-ci-cd'
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/ZeroDark-0/flask-ci-cd.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          docker.build("${IMAGE}")
        }
      }
    }

    stage('Push Docker Image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh """
            echo "$PASS" | docker login -u "$USER" --password-stdin
            docker push ${IMAGE}
          """
        }
      }
    }

    stage('Deploy (optional)') {
      steps {
        echo "Here you could SSH into a remote server and run Docker run"
      }
    }
  }
}
