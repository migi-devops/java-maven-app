pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                script {
                    echo 'Testing the application...'
                    echo "Executing pipeline for branch: $BRANCH_NAME"
                }
            }
        }
        stage('build') {
            when {
                expression {
                    BRANCH_NAME == "master"
                }
            }
            steps {
                script {
                    echo 'Building the application...'
                }
            }
        }
        stage('Deploy') {
            when {
                expression {
                    BRANCH_NAME == "master"
                }
            }
            steps {
                script {
                    echo 'Deploying...'
                }
            }
        }
    }
}
