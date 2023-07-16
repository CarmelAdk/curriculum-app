pipeline {
  agent any
  triggers {
    pollSCM '*/5 * * * *'
  }
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
            sh 'docker build -f curriculum-front/Dockerfile -t fuze365/curriculum-front:latest .'
          }
        }

        stage('Build Back End') {
          steps {
            sh 'docker build -f curriculum-back/Dockerfile -t fuze365/curriculum-back:latest .'
          }
        }

      }
    }

    stage('Log in to Dockerhub') {
      environment {
        DOCKERHUB_USER = 'fuze365'
        DOCKERHUB_PASSWORD = 'gv1&3Ea9W##onDQAMUG&41CvZ7h1d1'
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
      }
    }

    stage('Push Front End') {
      parallel {
        stage('Push Front End') {
          steps {
            sh 'docker push fuze365/curriculum-front:latest'
          }
        }

        stage('Push Back End') {
          steps {
            sh 'docker push fuze365/curriculum-back:latest'
          }
        }

      }
    }

  }
}
