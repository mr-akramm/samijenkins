pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Checkout code from your repository
            }
        }

        stage('S3 Upload') {
            steps {
                withAWS(region: 'us-east-1', credentials: 'a068f38a-acec-41d8-afe0-07cc9f0eb1a6') {
                    script {
                        // Check if the index.html file exists
                        def fileExists = sh(script: 'test -f index.html && echo "exists" || echo "not found"', returnStdout: true).trim()
                        if (fileExists == "not found") {
                            error "index.html not found in the workspace"
                        }

                        // Upload the index.html file to the S3 bucket
                        sh 'aws s3 cp index.html s3://jens-buc/'
                    }
                }
            }
        }
    }
}
