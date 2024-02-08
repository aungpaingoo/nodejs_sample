pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Install SSH client if not available
                    sh 'command -v ssh-agent >/dev/null || ( sudo apt-get update -y && sudo apt-get install openssh-client -y )'
                    // Start SSH agent
                    sshagent (credentials: ['WSL_SSH_PRIVATE_KEY']) {
                        // Build Docker image
                        sh '''
                            docker build -t jaft/my-node:latest .
                            docker login -u "$duser" -p "$dpw"
                            docker push jaft/my-node:latest
                        '''
                    }
                }
            }
        }
        stage('Deploy') {
            when {
                branch 'main' // Only deploy from the main branch
            }
            steps {
                script {
                    // Deploy the application
                    sshagent (credentials: ['WSL_SSH_PRIVATE_KEY']) {
                        sh "ssh -t '$usr@$server' 'mkdir GIT'"
                    }
                }
            }
        }
    }
}
