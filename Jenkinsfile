pipeline {
    agent any
    
    environment {
        EMAIL_RECIPIENT = 'neethuchandhavarkar2003@gmail.com'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Fetching the source code from Git repository'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Fetching the source code from DIRECTORY_PATH'
                echo 'Compile the code and generate any necessary artifacts'
                echo 'The code is built using the build automation tool named John'
                // Add your build steps here
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests'
                // Add your unit test command here

                echo 'Running integration tests'
                // Add your integration test command here
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Checking the quality of the code'
                echo 'SonarQube was used as a tool'
                // Add your code analysis steps here
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Running security scan'
                    // Replace the following line with your actual security scan command
                    sh 'security-scan-command'
                }
            }
        }

        stage('Deploy to Staging') {
            when {
                expression {
                    return currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                echo 'Deploying to staging environment'
                // Add your deployment steps here
            }
        }

        stage('Integration Tests on Staging') {
            when {
                expression {
                    return currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                echo 'Running integration tests on staging environment'
                // Add your staging integration tests here
            }
        }

        stage('Deploy to Production') {
            when {
                expression {
                    return currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                echo 'Deploying to production environment'
                // Add your production deployment steps here
            }
        }
    }

    post {
        always {
            emailext(
                to: EMAIL_RECIPIENT,
                subject: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} - Build # ${env.BUILD_NUMBER}",
                body: """
                <p>Build Details:</p>
                <p>Job Name: ${env.JOB_NAME}</p>
                <p>Build Number: ${env.BUILD_NUMBER}</p>
                <p>Build Status: ${currentBuild.currentResult}</p>
                <p>Build URL: ${env.BUILD_URL}</p>
                """,
                mimeType: 'text/html'
            )
        }
        failure {
            echo 'Build failed. Please check the logs for more details.'
        }
    }
}
