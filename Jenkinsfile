pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo '📥 Cloning Repository...'
                // Git checkout is auto-handled
            }
        }

        stage('Build Docker Image') {
            steps {
                echo '🐳 Building Docker image...'
                sh 'docker build -t flaskapp .'
            }
        }

        stage('Stop Old Container') {
            steps {
                echo '🛑 Stopping old container (if any)...'
                sh '''
                    docker stop flaskapp || true
                    docker rm flaskapp || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                echo '🚀 Running new container...'
                sh 'docker run -d -p 5000:5000 --name flaskapp flaskapp'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment complete!'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}

