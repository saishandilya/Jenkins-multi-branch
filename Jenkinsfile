pipeline {
    agent {
        label 'slave-node'
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/saishandilya/github-actions-project.git', branch: 'declarative'
            }
        }

        stage('Branch Validation') {
            steps {
                echo '✅ This is the declarative branch'
                sh 'git rev-parse --abbrev-ref HEAD'
            }
        }

        stage('Build & Generate Test Report') {
            steps {
                echo '🔧 Compiling, Generating test reports using Maven Surefire plugin and Building the application code using Apache Maven'
                sh '''
                    mvn compile
                    mvn test surefire-report:report
                    mvn clean package
                '''
            }
        }

        stage('Trivy FS Scan') {
            steps {
                echo '🔍 Running Trivy FS scan'
                sh 'trivy fs --format json -o fs-report.json .'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh 'cat README.md'
                sh 'echo Tests passed!'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying application...'
                sh 'echo Deploy complete!'
            }
        }
    }
}
