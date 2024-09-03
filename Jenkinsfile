pipeline {
    agent any
    environment {
        DIRECTORYPATH = "DIRECTORY_PATH"
        TESTINGENVIRONMENT = "TESTING_ENVIRONMENT"
        PRODUCTIONENVIRONMENT = "NeethuProdEnv"
    }
    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from ${DIRECTORYPATH}"
                echo "Compile the code and generate any necessary artifacts"
                echo "The code is built using the build automation tool named John"
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests"
                echo "Running integration tests"
                echo "John used the automation tool"
            }
            post {
                success {
                    emailext(
                        to: "neethuchandhavarkar2003@gmail.com",
                        subject: "Unit and Integration Tests Completed Successfully",
                        body: "Tests are completed successfully."
                    )
                }
                failure {
                    emailext(
                        to: "neethuchandhavarkar2003@gmail.com",
                        subject: "Unit and Integration Tests Failed",
                        body: "Some of the tests have failed. Please check the Jenkins build logs for details."
                    )
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo "Checking the quality of the code"
                echo "SonarQube was used as a tool"
            }
        }
        
        stage('Security Scan') {
            steps {
                script {
                    def securityScanOutput = sh(script: 'echo "Running VeraCode security scan..." && echo "VeraCode scan complete!" || true', returnStdout: true).trim()
                    echo securityScanOutput
                    env.SECURITY_SCAN_LOGS = securityScanOutput
                }
            }
            post {
                success {
                    emailext(
                        to: "neethuchandhavarkar2003@gmail.com",
                        subject: "Security Scan Completed Successfully",
                        body: "Security scan completed successfully.\n\nLogs:\n${env.SECURITY_SCAN_LOGS}",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: "neethuchandhavarkar2003@gmail.com",
                        subject: "Security Scan Failed",
                        body: "Security scan failed.\n\nLogs:\n${env.SECURITY_SCAN_LOGS}",
                        attachLog: true
                    )
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to a staging server"
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment to ensure the application functions as expected in a production-like environment"
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo "Deploying the code to ${PRODUCTIONENVIRONMENT}"
                echo "Deploying the application to a production server"
            }
        }
    }
    post {
        always {
            echo "Sending build notification email"
            emailext(
                to: "neethuchandhavarkar2003@gmail.com",
                subject: "Build ${currentBuild.currentResult}: ${currentBuild.fullDisplayName}",
                body: "Build ${currentBuild.fullDisplayName} completed with status: ${currentBuild.currentResult}. Check Jenkins for details.",
                attachLog: true
            )
        }
    }
}
