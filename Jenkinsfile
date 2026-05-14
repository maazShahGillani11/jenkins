pipeline {
    agent any

    environment {
        APP_NAME = "nextjs-app"
        EMAIL = "maazshahgillani02@gmail.com"
        PORT = "3000"
        APP_DIR = "/var/www/nextjs-app"
        NODE_ENV = "production"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/maazShahGillani11/jenkins'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Application') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    # Create deployment directory if it does not exist
                    sudo mkdir -p $APP_DIR

                    # Copy project files to deployment directory
                    sudo cp -r . $APP_DIR/

                    # Move into deployment directory
                    cd $APP_DIR

                    # Install production dependencies
                    sudo npm install --production

                    # Stop previous process if running
                    pkill -f "next start" || true

                    # Start application in background
                    nohup npm start > app.log 2>&1 &
                '''
            }
        }

    }

    post {
        success {
            echo 'Deployment completed successfully.'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}
