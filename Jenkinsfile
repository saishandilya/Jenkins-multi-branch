pipeline {
    agent {
        label 'slave-node'
    }

    stages {
        stage('Branch Validation') {
            steps {
                echo 'This is the main branch'
            }
        }

        stage('Checkout') {
            steps {
                git url: 'https://github.com/saishandilya/github-actions-project.git', branch: 'main'
            }
        }

        stage('Build & Generate Test Report') {
            steps {
                script {
                    echo 'Compiling, Generating test reports using Maven Surefire plugin and Building the application code using Apache Maven'
                    sh '''
                        mvn compile
                        mvn test surefire-report:report
                        mvn clean package
                    '''
                }
            }
        }

        stage('Trivy FS Scan') {
            steps {
                sh '''
                    echo "Trivy FS scan"
                    trivy fs --format table -o fs-report.json .
                '''
            }
        }
    }
}