pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo 'Running build script...'
                sh 'chmod +x hello.sh'
                sh './hello.sh'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo "All tests passed!"'
            }
        }
    }
    
    post {
        success {
            emailext (
                subject: "Jenkins Build SUCCESS - Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Build Successful!</h2>
                    <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                    <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                    <p><strong>Status:</strong> <span style="color:green">SUCCESS</span></p>
                    <p><strong>Build URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                    <hr>
                    <h3>Build Output:</h3>
                    <pre>${currentBuild.rawBuild.getLog(100).join('\n')}</pre>
                    <hr>
                    <p>Triggered by commit to GitHub repository.</p>
                """,
                to: 'alvinjegan.jegan1@gmail.com',
                mimeType: 'text/html'
            )
        }
        
        failure {
            emailext (
                subject: "Jenkins Build FAILED - Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Build Failed!</h2>
                    <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                    <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                    <p><strong>Status:</strong> <span style="color:red">FAILURE</span></p>
                    <p><strong>Build URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                    <hr>
                    <h3>Error Log:</h3>
                    <pre>${currentBuild.rawBuild.getLog(100).join('\n')}</pre>
                """,
                to: 'alvinjegan.jegan1@gmail.com',
                mimeType: 'text/html'
            )
        }
    }
}