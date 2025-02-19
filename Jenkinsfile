pipeline {
    agent any
    triggers {
        // This trigger listens to GitHub events, specifically tag pushes.
        githubPush()
    }
    environment {
        GIT_TAG = ""
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout the code
                    checkout scm
                    // Capture the tag name, if it's a tag push
                    GIT_TAG = sh(script: 'git describe --tags --abbrev=0', returnStdout: true).trim()
                }
            }
        }
        stage('Check Push Type') {
            steps {
                script {
                    // Get the Git tag (if any) and the current branch
                    def gitTag = sh(script: 'git describe --tags --abbrev=0', returnStdout: true).trim()
                    def currentBranch = env.BRANCH_NAME

                    // Check if the push is a Git tag or a branch push
                    if (gitTag) {
                        echo "Git Tag Push detected: ${gitTag}"
                    } else {
                        echo "Git Branch Push detected to branch: ${currentBranch}"
                    }
                }
            }
        }
        stage('Build') {
            steps {
                echo "Building the project for tag: ${GIT_TAG}"
                // Your build steps go here
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying the project for tag: ${GIT_TAG}"
                // Your deploy steps go here
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
