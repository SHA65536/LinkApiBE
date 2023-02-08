pipeline {
    agent {
        docker {
            image 'golang:latest'
        }
    }

    stages {
        stage('Build') {
            steps {
                sh "GOCACHE=/tmp/.cache"
                sh "export GOCACHE"
                sh "go env GOCACHE"
                // Build the application
                sh "go build ./cmd/linkapi"
            }
        }
        stage('Test') {
            steps {
                // Test the application
                sh "go test ./..."
            }
        }
        stage('Push') {
            steps {
                // Push to S3
                sh "aws s3 cp ./linkapi s3://cloudschoolproject-buildartifacts/linkapi"
            }
        }
    }
}