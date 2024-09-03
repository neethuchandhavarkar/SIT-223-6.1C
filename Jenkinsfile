pipeline {
    agent any
    environment {
        DIRECTORYPATH = "DIRECTORY_PATH"
        TESTINGENVIRONMENT = "TESTING_ENVIRONMENT"
        PRODUCTIONENVIRONMENT = "NeethuProdEnv"
    }
    triggers {
        pollSCM('H/5 * * * *')  // Poll the SCM every 5 minutes to check for new commits
    }
    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from ${DIRECTORYPATH}"
                echo "Building the code using Maven or Gradle"
                echo "Compile and package the code"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests using JUnit or TestNG"
                echo "Running integration tests to ensure all components work together"
            }
            post {
                success {
                    emailext(
                        to: 'neethuchandhavarkar2003@gmail.com',
                        subject: "Unit and Integration Tests - SUCCESS",
                        body: "The Unit and Integration Tests have completed successfully.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: 'neethuchandhavarkar2003@gmail.com',
                        subject: "Unit and Integration Tests - FAILURE",
                        body: "The Unit and Integration Tests have failed.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Performing code analysis using SonarQube"
                echo "Analyzing code quality and ensuring industry standards"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Performing security scan using Veracode"
                echo "Identifying vulnerabilities in the code"
            }
            post {
                success {
                    emailext(
                        to: 'neethuchandhavarkar2003@gmail.com',
                        subject: "Security Scan - SUCCESS",
                        body: "The Security Scan has completed successfully.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: 'neethuchandhavarkar2003@gmail.com',
                        subject: "Security Scan - FAILURE",
                        body: "The Security Scan has failed.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to the staging server (e.g., AWS EC2)"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment"
                echo "Ensuring the application functions as expected in a production-like environment"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying the application to the production server (e.g., AWS EC2)"
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed"
        }
    }
}
