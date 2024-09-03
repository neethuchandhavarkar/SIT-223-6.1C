pipeline {
    agent any
    environment {
        DIRECTORYPATH = "DIRECTORY_PATH"
        TESTINGENVIRONMENT = "TESTING_ENVIRONMENT"
        PRODUCTIONENVIRONMENT = "NeethuProdEnv"
        LOGFILE = "build_log.txt"
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
            // Save the build log to a file
            script {
                def logContent = currentBuild.rawBuild.getLog(1000).join("\n")
                writeFile file: "${LOGFILE}", text: logContent
            }
            // Send the email with the log file attached
            mail to: "neethuchandhavarkar2003@gmail.com",
                 subject: "Build Status: ${currentBuild.currentResult}",
                 body: "The build has completed with status: ${currentBuild.currentResult}. Please find the log attached.",
                 attachLog: true,
                 attachmentsPattern: "${LOGFILE}"
        }
    }
}
