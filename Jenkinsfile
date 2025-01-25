node {
    docker.image('node:16-buster-slim').withRun('-p 3000:3000') { container ->
        env.CI = 'true'
        try {
            stage('Checkout') {
                checkout scm
            }

            stage('Build') {
                echo 'Starting Build stage...'
                dir('react-app') { // Adjust if necessary
                    sh 'ls -la' // Debugging step
                    sh 'node -v' // Check Node version
                    sh 'npm -v' // Check npm version
                    sh 'npm install'
                }
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