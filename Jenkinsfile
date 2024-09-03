pipeline {
    agent any
    
    environment {
        // Define any environment variables needed here
    }

    stages {
        stage('Checkout SCM') {
            steps {
                echo 'Checking out source code from Git repository'
                checkout([$class: 'GitSCM', 
                          userRemoteConfigs: [[url: 'https://github.com/neethuchandhavarkar/SIT-223-6.1C']],
                          scm: [$class: 'GitSCM', 
                                userRemoteConfigs: [[url: 'https://github.com/neethuchandhavarkar/SIT-223-6.1C']],
                                branches: [[name: '*/main']]
                          ]])
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building the project'
                echo 'Fetching the source code from the directory'
                echo 'Compiling the code and generating necessary artifacts'
                echo 'Using build automation tool named John'
                // Add your build commands here
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests'
                echo 'Running integration tests'
                echo 'Using automation tool John'
                // Add your test commands here
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality'
                echo 'Using SonarQube for code analysis'
                // Add your code analysis commands here
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    try {
                        echo 'Performing security scan'
                        // Add your security scan commands here
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        echo "Security scan failed: ${e.message}"
                    }
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
                // Add your deployment commands here
            }
        }

        stage('Integration Tests on Staging') {
            when {
                expression {
                    return currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                echo 'Running integration tests on staging'
                // Add your integration test commands here
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
                // Add your production deployment commands here
            }
        }
    }

    post {
        always {
            echo 'Sending email notification'
            mail to: 'neethuchandhavarkar2003@gmail.com',
                 subject: "Build ${currentBuild.currentResult}: ${currentBuild.fullDisplayName}",
                 body: "Build ${currentBuild.fullDisplayName} completed with status: ${currentBuild.currentResult}. Check Jenkins for details.",
                 attachmentsPattern: '**/build/logs/*.log'  // Adjust the pattern to match your log files
        }
        failure {
            echo 'Build failed'
            mail to: 'neethuchandhavarkar2003@gmail.com',
                 subject: "Build FAILED: ${currentBuild.fullDisplayName}",
                 body: "Build ${currentBuild.fullDisplayName} failed. Check Jenkins for details.",
                 attachmentsPattern: '**/build/logs/*.log'  // Adjust the pattern to match your log files
        }
    }
}
