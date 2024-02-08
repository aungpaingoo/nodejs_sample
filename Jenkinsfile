pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository
                git 'git@github.com:aungpaingoo/nodejs_sample.git'
                // Save code to a directory
                dir('my-directory') {
                    sh 'cp -r * ../my-directory' // Copy all files and directories to 'my-directory'
                }
            }
        }
        
        // Add additional stages for building, testing, etc.
    }
}
