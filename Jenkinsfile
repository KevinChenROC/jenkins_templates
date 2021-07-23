Jenkinsfile (Declarative Pipeline)
//a typical template for declarative pipeline

pipeline {
    agent any  // An agent is typically a machine, or container, which connects to a Jenkins controller and executes tasks when directed by the controller.


    environment {
        DB_ENGINE    = 'sqlite' //user-defined env variable
    }

    stages {
        stage('build'){
            steps{
                echo "Database engine is ${DB_ENGINE}"
                sh 'echo "run build tasks'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "run test tasks"'
            }
        }

        stage('Deploy - Staging') {
            steps {
                //sh './deploy staging'
                //sh './run-smoke-tests'
            }
        }

        stage('Sanity check') {
            steps {
                input "Does the staging environment look ok?"
            }
        }

        stage('Deploy - Production') {
            steps {
                //sh './deploy production'
            }
        }

    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
            
            //send messages by mails, slack, etc.
            mail to: 'team@example.com',
            //env and currentBuild are the global variables visible to all in the pipeline
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}" 
    }
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
