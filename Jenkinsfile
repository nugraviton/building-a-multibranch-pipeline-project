pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'build stage for all branches.'
            }
        }
        stage('Unit testing for development branch') {
            when {
                branch 'development'
            }
            steps {
                echo 'only for development branch'                
            }
        }
        
        stage('nightly build for master branch ') {
            when {
                branch 'development'
            }
            steps {                
                    echo 'only for development branch'                                
            }
        }
        
        
        stage('production build') {
            when {
                branch 'production'
            }
            steps{
                env.PROD_DEPLOYMENT = input message: 'User input required',
                    parameters: [
                            choice(name: 'Production release?', 
                            choices: 'no\nyes', 
                            description: 'Choose "yes" if you want to release to official production')]               
            
            if(PROD_DEPLOYMENT == 'yes'){
                echo 'Deployed on production!'
            }
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
    post {
      always{
          echo 'I will always say Hello again!'
      }
      failure {
        mail to: 'fred.wang@bcldb.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
    }
}
}
