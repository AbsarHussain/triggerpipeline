pipeline {
    agent any
    triggers {
        // Trigger the pipeline on any Git tag push
        // The pattern `*` means any tag will trigger this pipeline
        gitTag('*')
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository to access the git history
                checkout scm
            }
        }
        stage('Print Git Tag') {
            steps {
                script {
                    // Get the name of the pushed Git tag
                    def gitTag = sh(script: 'git describe --tags --abbrev=0', returnStdout: true).trim()
                    
                    // Print the Git tag to the console
                    echo "The pushed Git tag is: ${gitTag}"
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
