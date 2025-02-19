pipeline {
    agent any
    triggers {
        // Trigger the pipeline when a GitHub push event happens (including tags)
        githubPush() 
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository to access the Git history
                checkout scm
            }
        }
        stage('Check for Git Tag') {
            steps {
                script {
                    // Get the latest Git tag (if any)
                    def gitTag = sh(script: 'git describe --tags --abbrev=0', returnStdout: true).trim()
                    
                    // If a tag exists, print it
                    if (gitTag) {
                        echo "The pushed Git tag is: ${gitTag}"
                    } else {
                        echo "No Git tag found in the current commit."
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeli
