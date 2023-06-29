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
      steps {
        sh 'cd curriculum-front && npm i && npm run test:unit'
      }
    }

  }
}