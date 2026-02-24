// creating a pipelone for jenkins
pipeline {
    agent any
    parameters {
        string(name: 'ENVIRONMENT', defaultValue: 'dev', description: 'Environment to deploy to')
        choice(name: 'deploy', description: 'Deploy to production', choices: ['dev', 'staging', 'prod'])

        }
    environment {
        course = 'jenkins'
        }
    // options {
    //     timeout(time: 20, unit: 'seconds')
    //     }    
        
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sleep 5
            }
        }

        stage('Test') {
            steps {
                script {
                    sh """
                    echo 'environment is ${params.ENVIRONMENT}'
                    env
                    """
                }
                echo 'Testing...'
                echo 'testing github webhooks'
            }
        }

        stage('Deploy') {
            when {
                    expression { return params.deploy == 'prod' }
                }
            steps {
                 echo "since the choice in parameters is: ${params.deploy} Deploying..."
            }
        }
    }
     post {
            always {
                echo 'This will always run'
                cleanWs()
            }
            success {
                echo 'This will run only if successful'
            }
            failure {
                echo 'This will run only if failed'
            }
            aborted {
                echo 'This will run only if aborted'
            }
        }

}