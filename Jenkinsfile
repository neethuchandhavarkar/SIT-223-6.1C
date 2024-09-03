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
                echo "The code is built using the automation tool named John"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Run unit tests"
                echo "Run integration tests"
                echo "John is used as the automation tool"
            }
            post {
                success {
                    mail to: "neethuchandhavarkar2003@gmail.com",
                         subject: "Test Status Email",
                         body: "Tests have been completed successfully."
                }
                failure {
                    mail to: "neethuchandhavarkar2003@gmail.com",
                         subject: "Test Status Email - Failed",
                         body: "Tests have failed. Please check the build logs."
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Check the quality of the code"
                echo "SonarQube was used as a tool"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Veracode used for security scan"
            }
            post {
                success {
                    mail to: "neethuchandhavarkar2003@gmail.com",
                         subject: "Security Scan Status",
                         body: "Security scan has been completed successfully."
                }
                failure {
                    mail to: "neethuchandhavarkar2003@gmail.com",
                         subject: "Security Scan Status - Failed",
                         body: "Security scan has failed. Please review the scan results."
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploy the application to a staging server"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Run integration tests on the staging environment to ensure the application functions as expected in a production-like environment"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploy the code to ${PRODUCTIONENVIRONMENT}"
                echo "Deploy the application to a production server"
            }
        }
    }
}
