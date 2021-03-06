pipeline {
    agent any
    environment {
        DEPLOY_STAGING = 'no'
        DEPLOY_PRODUCTION    = 'no'
    }
    
  stages {
        stage('Build') {
            steps {
                echo 'build stage for all branches.'
            }
         }
      
         stage('Test') {
            steps {
                echo 'only for development branch'                
            }
         }
        
        stage('Deploy - Devlopment') {
            when {
                branch 'development'
            }
            steps {                
                    echo 'only for development branch'                                
            }
         }
                
        stage('Deloy - Staging') {            
            environment {
              DEPLOY_STAGING = input message: 'Deploy to staging?',
                  parameters: [
                            choice(name: 'Deploy to staging?', 
                            choices: 'no\nyes', 
                            description: 'Choose "yes" if you want to deploy to staging')]    
            }
            when {
                allOf {
                  branch 'production'
                  environment name: 'DEPLOY_STAGING', value: 'yes'
                }
            }
            
            steps{
                echo 'deploy to staging executed.'
           }
        }
        
        stage('Deploy - Production') {
            
            environment {
              DEPLOY_PRODUCTION = input message: 'Deploy to production?',
                  parameters: [
                            choice(name: 'Deploy to production?', 
                            choices: 'no\nyes', 
                            description: 'Choose "yes" if you want to deploy to production')]                           
            }
            when {
                allOf {
                  branch 'production'
                  environment name: 'DEPLOY_PRODUCTION', value: 'yes'
                }
            }
            
            steps{
                echo 'deploy to production executed.'
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
