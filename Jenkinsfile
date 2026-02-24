// creating a pipelone for jenkins
pipeline {
    agent any
    environment {
        ENV = 'dev'
    }
        timeout(time: 4, unit: 'seconds')
        parameters {
        string(name: 'ENV', defaultValue: 'dev', description: 'Environment to deploy to')
        text(name: 'deploy', description: 'Deploy to production', choices: ['dev', 'staging', 'prod'])

    }
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
                    echo 'environment is ${ENV}'
                    env
                    """
                }
                echo 'Testing...'
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