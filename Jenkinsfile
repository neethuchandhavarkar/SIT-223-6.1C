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

    post {
        always {
            script {
                def logContent = currentBuild.rawBuild.getLog(100) // Gets the last 100 lines of the build log
                emailext(
                    to: 'neethuchandhavarkar2003@gmail.com',
                    subject: "Build Status: ${currentBuild.currentResult}",
                    body: "The build has completed with status: ${currentBuild.currentResult}. Please find the attached log file.",
                    attachLog: true
                )
            }
        }
    }
}
