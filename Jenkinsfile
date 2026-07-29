pipeline {

    agent any

    environment {
        BUCKET = "gs://YOUR_BUCKET_NAME"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/YOUR_USERNAME/simple-html.git'
            }
        }

        stage('Build') {
            steps {
                sh '''
                mkdir -p build
                cp *.html build/
                cp *.css build/
                '''
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'build/**'
            }
        }

        stage('Upload to GCS') {
            steps {
                sh '''
                gsutil -m cp -r build/* $BUCKET
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment Successful"
        }

        failure {
            echo "Deployment Failed"
        }
    }
}
