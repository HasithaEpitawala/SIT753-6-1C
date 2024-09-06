pipeline {
    agent any

    environment {
        DIRECTORY_PATH = "C:/Program Files/Java/jdk-17"
        TESTING_ENVIRONMENT = "DevelopmentEnv"
        PRODUCTION_ENVIRONMENT = "hasitha_production_env"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo "Fetching source code from ${env.DIRECTORY_PATH}"
                    echo "Compiling code and creating artifacts"
                    echo "Tools: Maven, ANT"
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo "Run unit tests"
                    echo "Run integration tests"
                    echo "Tools: Junits, TestNG"
                }
            }
        }
        stage('Code Quality Check') {
            steps {
                script {
                    echo "Check the quality of the code"
                    echo "Tools: SonarQube, Checkstyle"
                }
            }
            post {
                success {
                    emailext to: 'hasitha.epitawala@gmail.com',
                             subject: "Testing ${currentBuild.result}: ${currentBuild.fullDisplayName}",
                             body: "testing status: ${currentBuild.result}.\n" +
                                   "Check the attached logs for more details.",
                             attachLog: true
                }
                failure {
                    emailext to: 'hasitha.epitawala@gmail.com',
                             subject: "Testing ${currentBuild.result}: ${currentBuild.fullDisplayName}",
                             body: "testing status: ${currentBuild.result}.\n" +
                                   "Check the attached logs for more details.",
                             attachLog: true
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo "Deploying to testing environment: ${env.TESTING_ENVIRONMENT}"
                    echo "Tools: Kubernetes, Ansible"
                }
            }
        }
        stage('Approval') {
            steps {
                script {
                    echo "Waiting for manual approval...!"
                    sleep(time: 10, unit: 'SECONDS')
                    echo "Tools: Jenkins Input Step, Ansible"
                }
            }
            post {
                success {
                    emailext to: 'hasitha.epitawala@gmail.com',
                             subject: "Testing ${currentBuild.result}: ${currentBuild.fullDisplayName}",
                             body: "testing status: ${currentBuild.result}.\n" +
                                   "Check the attached logs for more details.",
                             attachLog: true
                }
                failure {
                    emailext to: 'hasitha.epitawala@gmail.com',
                             subject: "Testing for security scan ${currentBuild.result}: ${currentBuild.fullDisplayName}",
                             body: "testing status for security scan: ${currentBuild.result}.\n" +
                                   "Check the attached logs for more details.",
                             attachLog: true
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploying to production: ${env.PRODUCTION_ENVIRONMENT}"
                    echo "Tools: AWS, Kubernetes"
                }
            }
        }
        
    }
}
// Git comment
