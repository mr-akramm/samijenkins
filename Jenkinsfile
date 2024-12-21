pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Checks out the source code from your GitHub repo
            }
        }

        stage('S3 Upload') {
            steps {
                withAWS(region: 'ap-south-1', credentials: 'c6f685f1-0f87-4962-bf2e-72e9bd59f7a5') {
                    script {
                        // List contents to verify files are available
                        sh 'ls -la'

                        // Check if the file index.html exists in the workspace
                        def fileExists = sh(script: 'test -f index.html && echo "exists" || echo "not found"', returnStdout: true).trim()
                        if (fileExists == "not found") {
                            error "index.html not found in the workspace"
                        }

                        // Upload the index.html file to the S3 bucket
                        sh 'aws s3 cp index.html s3://sami22/'

                        // Optionally, you can upload additional assets (like CSS, JS, etc.)
                        // sh 'aws s3 cp ./assets/ s3://sami22/assets/ --recursive'
                    }
                }
            }
        }
    }
}
