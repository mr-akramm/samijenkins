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
                withAWS(region: 'us-east-1', credentials: 'c6f685f1-0f87-4962-bf2e-72e9bd59f7a5') {
                    sh '''
                        # List contents to verify files are available
                        ls -la

                        # Upload the index.html file to the S3 bucket 
                        aws s3 cp index.html s3://xprepo-bucket/

                        # Optionally, you can upload additional assets (like CSS, JS, etc.)
                        # aws s3 cp ./assets/ s3://xprepo-bucket/assets/ --recursive
                    '''
                }
            }
        }
    }
}
