pipeline {
  agent any
  stages {
    stage('Checkout Code ') {
      steps {
        git(url: 'https://github.com/CarmelAdk/curriculum-app', branch: 'dev')
      }
    }

    stage('Log') {
      steps {
        sh 'ls -la'
        sh 'echo $USER'
      }
    }

    stage('Front End Unit Tests') {
      parallel {
        stage('Front End Unit Tests') {
          steps {
            sh 'cd curriculum-front'
          }
        }

        stage('Back End Unit Test') {
          steps {
            sh 'cd curriculum-back'
          }
        }

      }
    }

    stage('Build Front End') {
      parallel {
        stage('Build Front End') {
          steps {
            sh 'docker build -f curriculum-front/Dockerfile .'
          }
        }

        stage('Build Back End') {
          steps {
            sh 'docker build -f curriculum-back/Dockerfile .'
          }
        }

      }
    }

    stage('Log in to Dockerhub') {
      environment {
        DOCKERHUB_USER = 'carmeladikin'
        DOCKERHUB_PASSWORD = 'Dockerhub04@'
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
      }
    }

  }
}