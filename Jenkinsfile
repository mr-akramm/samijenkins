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
                withAWS(region: 'us-east-1', credentials: '98d79972-7945-482f-8dc8-ad27413cecb5') {
                    script {
                        // Check if the index.html file exists
                        def fileExists = sh(script: 'test -f index.html && echo "exists" || echo "not found"', returnStdout: true).trim()
                        if (fileExists == "not found") {
                            error "index.html not found in the workspace"
                        }

                        // Upload the index.html file to the S3 bucket
                        sh 'aws s3 cp index.html s3://pro1110/'
                    }
                }
            }
        }
    }
}
