pipeline {
    agent any

    environment {
        // Define environment variables if needed
        // Example: PATH = "/usr/local/bin:$PATH"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from version control
                git url: 'https://github.com/your-repo.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Example build step
                sh './gradlew build'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh './gradlew test'
            }
            post {
                always {
                    // Archive test results
                    junit '**/build/test-results/test/*.xml'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Example deploy step
                sh './deploy.sh'
            }
        }
    }

    post {
        always {
            // Clean up resources, send notifications, etc.
            cleanWs()
        }
        success {
            // Actions to take if the build is successful
            mail to: 'team@example.com',
                 subject: "Successful Build: ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                 body: "Good news! The build was successful. Check out the details at ${env.BUILD_URL}"
        }
        failure {
            // Actions to take if the build fails
            mail to: 'team@example.com',
                 subject: "Failed Build: ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                 body: "Something went wrong. The build failed. Check out the details at ${env.BUILD_URL}"
        }
    }
}
