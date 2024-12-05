pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'your-email@example.com'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                    echo 'Building the project...'
                    sh 'python hello.py'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    sh 'pytest'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying to GitHub...'
                    sh '''
                    git config --global user.email "you@example.com"
                    git config --global user.name "Your Name"
                    git add .
                    git commit -m "Automated commit by Jenkins"
                    git push origin main
                    '''
                }
            }
        }
    }

    post {
        always {
            script {
                echo 'Sending email notification...'
                mail to: "${EMAIL_RECIPIENT}",
                     subject: "Build ${currentBuild.fullDisplayName}",
                     body: "The build ${currentBuild.fullDisplayName} has completed. Please check the Jenkins console for details."
            }
        }
    }
}
