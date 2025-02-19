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
        stage('Print Webhook Metadata') {
            steps {
                script {
                    // Print general webhook metadata using environment variables
                    echo "Webhook event: ${env.GIT_URL}"
                    echo "Repository: ${env.GIT_COMMITTER_NAME}"
                    echo "Commit ID: ${env.GIT_COMMITTER_EMAIL}"
                    echo "Branch: ${env.BRANCH_NAME}"
                    echo "GitHub Event: ${env.GITHUB_EVENT_NAME}"  // GitHub event type (e.g., push, pull_request)
                    echo "GitHub Ref: ${env.GITHUB_REF}"  // Git reference (e.g., refs/heads/main)

                    // If more metadata is available (depending on your GitHub webhook payload)
                    echo "Commit message: ${env.GIT_AUTHOR_NAME}" 
                    echo "Commit hash: ${env.GIT_COMMIT}"
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
