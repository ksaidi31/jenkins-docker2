pipeline {
  agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }

  environment {
    DOCKERHUB_CREDENTIALS = credentials('ksaidi')
  }

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t ksaidi/image_docker .'
      }
    }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push ksaidi/image_docker'
      }
    }
  }

  post {
    always {
      script {
        sh 'docker logout'
      }
    }
  }
}
