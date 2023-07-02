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
            sh 'docker build -f curriculum-front/Dockerfile -t fuze365/curriculum-front .'
          }
        }

        stage('Build Back End') {
          steps {
            sh 'docker build -f curriculum-back/Dockerfile -t fuze365/curriculum-back .'
          }
        }

      }
    }

    stage('Log in to Dockerhub') {
      environment {
        DOCKERHUB_PASSWORD = 'gv1&3Ea9W##onDQAMUG&41CvZ7h1d1'
        DOCKERHUB_USER = 'fuze365'
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
      }
    }

  }
}