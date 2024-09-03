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
                echo "fetch the source code from the ${DIRECTORYPATH}"
                echo "compile the code and generate any necessary artifacts"
                echo "The code is built using the build automation tool named John"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "unit tests"
                echo "integration test"
                echo "john used the automation tool"
            }
            post {
                success {
                    mail to: "neethuchandhavarkar2003@gmail.com",
                        subject: "test status email",
                        body: "test is completed"
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "check the quality of the code"
                echo "SonarQube was used as a tool"
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    def securityScanOutput = sh(script: 'echo "Running VeraCode security scan..." && echo "VeraCode scan complete!"', returnStdout: true).trim()
                    echo securityScanOutput
                    env.SECURITY_SCAN_LOGS = securityScanOutput
                }
            }
            post {
                success {
                    mail to: "neethuchandhavarkar2003@gmail.com",
                        subject: "Security scan stage ${currentBuild.result}",
                        body: "Security scan completed successfully.\n\nLogs:\n${env.SECURITY_SCAN_LOGS}"
                }
                failure {
                    mail to: "neethuchandhavarkar2003@gmail.com",
                        subject: "Security scan stage ${currentBuild.result}",
                        body: "Security scan failed.\n\nLogs:\n${env.SECURITY_SCAN_LOGS}"
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "In Jenkins - deploy the application to a staging server"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Run the integration tests on the staging environment to ensure the application functions as expected in a production-like environment"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "DEPLOY the code to ${PRODUCTIONENVIRONMENT}"
                echo "Deploy the application to a production server"
            }
        }
    }
}
