pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'echo "Hello world!"'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {

                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                bat 'echo "stage for development"'
            }
        }
        stage('nightly build') {
            when {
                branch 'master'
            }
            steps {

                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                bat 'echo "stage for master"'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {

                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                bat 'echo "stage for procuction"'
            }
        }
    }
}
