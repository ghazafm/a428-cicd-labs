node {
    docker.image('node:16-buster-slim').withRun('-p 3000:3000').inside { container ->
        env.CI = 'true'
        try {
            stage('Build') {
                echo 'Starting Build stage...'
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