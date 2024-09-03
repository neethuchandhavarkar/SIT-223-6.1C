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
                // Example command to create a log file
                sh 'echo "Build logs" > logs/build.log'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "unit tests"
                echo "integration tests"
                echo "John used the automation tool"
                // Example command to create a log file
                sh 'echo "Test logs" > logs/test.log'
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
                // Example command to create a log file
                sh 'echo "Code analysis logs" > logs/code_analysis.log'
                // Archive the logs
                archiveArtifacts artifacts: 'logs/**/*', allowEmptyArchive: true
            }
        }

        stage('Security Scan') {
            steps {
                echo "Veracode used for security scan"
                // Example command to create a log file
                sh 'echo "Security scan logs" > logs/security_scan.log'
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
                // Example command to create a log file
                sh 'echo "Deploy to staging logs" > logs/deploy_staging.log'
                // Archive the logs
                archiveArtifacts artifacts: 'logs/**/*', allowEmptyArchive: true
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "run the integration tests on the staging environment to ensure the application functions as expected in a production-like environment"
                // Example command to create a log file
                sh 'echo "Integration tests on staging logs" > logs/integration_tests_staging.log'
                // Archive the logs
                archiveArtifacts artifacts: 'logs/**/*', allowEmptyArchive: true
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "DEPLOY the code to ${PRODUCTIONENVIRONMENT}"
                echo "Deploy the application to a production server"
                // Example command to create a log file
                sh 'echo "Deploy to production logs" > logs/deploy_production.log'
                // Archive the logs
                archiveArtifacts artifacts: 'logs/**/*', allowEmptyArchive: true
            }
        }
    }
    post {
        always {
            emailext(
                to: 'neethuchandhavarkar2003@gmail.com',
                subject: "Pipeline Logs",
                body: "The pipeline has completed. Please find the attached logs.",
                attachmentsPattern: 'logs/**/*'
            )
        }
    }
}
