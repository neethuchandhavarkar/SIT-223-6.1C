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
                echo "integration tests"
                echo "John used the automation tool"
                // Archive the logs
                archiveArtifacts artifacts: 'logs/**/*', allowEmptyArchive: true
            }
            post {
                success {
                    emailext(
                        to: 'neethuchandhavarkar2003@gmail.com',
                        subject: "Test Status Email",
                        body: "Test is completed",
                        attachmentsPattern: 'logs/**/*'
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "check the quality of the code"
                echo "SonarQube was used as a tool"
                // Archive the logs
                archiveArtifacts artifacts: 'logs/**/*', allowEmptyArchive: true
            }
        }

        stage('Security Scan') {
            steps {
                echo "Veracode used for security scan"
                // Archive the logs
                archiveArtifacts artifacts: 'logs/**/*', allowEmptyArchive: true
            }
            post {
                success {
                    emailext(
                        to: 'neethuchandhavarkar2003@gmail.com',
                        subject: "Security Scan Stage ${currentBuild.result}",
                        body: "Security scan completed",
                        attachmentsPattern: 'logs/**/*'
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "In Jenkins-deploy the application to a staging server"
                // Archive the logs
                archiveArtifacts artifacts: 'logs/**/*', allowEmptyArchive: true
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "run the integration tests on the staging environment to ensure the application functions as expected in a production-like environment"
                // Archive the logs
                archiveArtifacts artifacts: 'logs/**/*', allowEmptyArchive: true
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "DEPLOY the code to ${PRODUCTIONENVIRONMENT}"
                echo "Deploy the application to a production server"
                // Archive the logs
                archiveArtifacts artifacts: 'logs/**/*', allowEmptyArchive: true
            }
        }
    }
    post {
        always {
            // Optional: send an email with all logs as attachments, if needed
            emailext(
                to: 'neethuchandhavarkar2003@gmail.com',
                subject: "Pipeline Logs",
                body: "The pipeline has completed. Please find the attached logs.",
                attachmentsPattern: 'logs/**/*'
            )
        }
    }
}
