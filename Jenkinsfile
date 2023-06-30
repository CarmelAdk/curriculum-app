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
        sh 'ls'
      }
    }

    stage('Front End Unit Tests') {
      parallel {
        stage('Front End Unit Tests') {
          steps {
            sh 'cd curriculum-front && npm install'
          }
        }

        stage('Back End Unit Test') {
          steps {
            sh 'cd curriculum-back && npm install'
          }
        }

      }
    }

  }
}