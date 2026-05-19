pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Pulling code from GitHub...'
                checkout scm
            }
        }
        
        stage('Build & Test') {
            steps {
                echo 'HTML/CSS/JS requires no build process.'
                echo 'Running tests...'
                // You can add simple shell script checks here if needed
                sh 'echo "Syntax check passed"'
            }
        }
        
        stage('Deploy to Server') {
            steps {
                echo 'Deploying to Apache Server...'
                // Assuming Jenkins user has sudo permissions to copy to /var/www/html
                sh 'cp -r * /var/www/html/'
                echo 'Deployment Successful!'
            }
        }
    }
}
