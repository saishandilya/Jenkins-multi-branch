node('slave-node') {

    stage('Checkout') {
        git url: 'https://github.com/saishandilya/Jenkins-multi-branch.git', branch: 'scripted'
    }

    stage('Branch Validation') {
        echo '✅ This is the scripted branch'
        sh 'git rev-parse --abbrev-ref HEAD'
    }

    stage('Build & Generate Test Report') {
        echo '🔧 Compiling, Generating test reports using Maven Surefire plugin and Building the application code using Apache Maven'
        sh '''
            mvn compile
            mvn test surefire-report:report
            mvn clean package
        '''
    }

    stage('Trivy FS Scan') {
        echo '🔍 Running Trivy filesystem scan...'
        sh '''
            trivy fs --format json -o fs-report.json .
        '''
    }

    stage('Test') {
        echo '🧪 Running tests...'
        sh 'cat README.md'
        sh 'echo Tests passed!'
    }

    stage('Deploy') {
        echo '🚀 Deploying application...'
        sh 'echo Deploy complete!'
    }
}