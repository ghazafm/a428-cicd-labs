node {
    docker.image('node:16').withRun('-p 3000:3000' '--user root') { container ->
        env.CI = 'true'
        try {
            stage('Checkout') {
                checkout scm
            }

            stage('Check Environment') {
            echo 'Checking if node and npm are installed...'
            sh 'which node || echo "Node not found"'
            sh 'which npm || echo "NPM not found"'
            sh 'node -v || echo "Node version not found"'
            sh 'npm -v || echo "NPM version not found"'
            }

            stage('Build') {
                echo 'Starting Build stage...'
                sh 'apt-get update && apt-get install nodejs npm -y'
                sh 'npm install'
            }

            stage('Test') {
                echo 'Starting Test stage...'
                sh './jenkins/scripts/test.sh'
            }
        } catch (Exception e) {
            error "Pipeline failed: ${e.getMessage()}"
        }
    }
}