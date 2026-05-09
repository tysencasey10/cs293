pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-2'
        S3_BUCKET = 'tysen-cs293-static-site'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify files') {
            steps {
                sh 'ls -l'
            }
        }

        stage('Deploy to S3') {
            steps {
                sh '''
                aws s3 sync . s3://$S3_BUCKET \
                  --delete \
                  --exclude ".git/*" \
                  --exclude "Jenkinsfile" \
                  --exclude "jenkinsfile" \
                  --exclude "README.md" \
                  --exclude "readme.txt" \
                  --exclude "pom.xml" \
                  --exclude "*.java"
                '''
            }
        }
    }
}
