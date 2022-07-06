pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/ChrisBarnes2000-Revature/flask-demo.git'
                // Run venv
                sh "python3 -m venv .venv"
                // Run pip install
                sh "pip3 install -r requirements-dev.txt"
                // Run pytest
                sh "python3 -m pytest app-test.py"
            }
        }
        stage ('Discord') {
            steps{
                discordSend description: 'Hello Discord', enableArtifactsList: true, footer: '', image: '', link: 'env.BUILD_URL', result: 'SUCCESS', scmWebUrl: '', thumbnail: '', title: 'Project1', webhookURL: 'https://discord.com/api/webhooks/994018555341307966/V-Or2AnFnDNpfHa7slRrl2S0rhdybzYSnDNzKHVHgnKxJHCWG8iXWVQAPNjsa8hvHJ_q'
            }
        }
    }
}
