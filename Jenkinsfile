pipeline {
    agent {
        docker {
            image 'node:16-buster-slim' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install'
            }
        }
    }
    stages {
        stage('Test') { 
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
    }
}