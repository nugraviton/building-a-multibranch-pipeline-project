pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            bat 'echo "Hello world!"'
          }
        }
        stage('test') {
          steps {
            bat 'echo "hello, testing..."'
          }
        }
      }
    }
    stage('Deliver for development') {
      when {
        branch 'development'
      }
      steps {
        input 'Finished using the web site? (Click "Proceed" to continue)'
        bat 'stage for development'
      }
    }
    stage('Deploy for production') {
      when {
        branch 'production'
      }
      steps {
        input 'Finished using the web site? (Click "Proceed" to continue)'
        bat 'stage for procuction'
      }
    }
  }
}