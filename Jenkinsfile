pipeline {
    agent any
    // agent { dockerfile true }

    stages {
        stage('Start') {
            echo 'Running ${env.BUILD_ID} on ${env.JENKINS_URL}'
        }
        stage('Build') {
            steps {
                echo 'Building..'
                // Get some code from a GitHub repository
                git 'https://github.com/ChrisBarnes2000-Revature/flask-demo.git'
                // Run venv
                sh 'python3 -m venv .venv'
                // Run pip install
                sh 'pip3 install -r requirements-dev.txt'
            }
        }
        stage('Lint') {
            steps {
                echo 'Linting..'
                // stop the build if there are Python syntax errors or undefined names
                sh 'flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics'
                // exit-zero treats all errors as warnings. The GitHub editor is 127 chars wide
                sh 'flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                // Run pytest
                sh 'python3 -m pytest app-test.py'
            }
        }
        stage ('Discord') {
            steps{
                echo 'Post Deploy Messaging....'
                discordSend description: 'Hello Discord', enableArtifactsList: true, footer: '', image: '', link: 'env.BUILD_URL', result: 'SUCCESS', scmWebUrl: '', thumbnail: '', title: 'Project1', webhookURL: 'https://discord.com/api/webhooks/994018555341307966/V-Or2AnFnDNpfHa7slRrl2S0rhdybzYSnDNzKHVHgnKxJHCWG8iXWVQAPNjsa8hvHJ_q'
            }
        }
    }
    post {
        always {
            junit '**/target/*.xml'
        }
        failure {
            mail to: Chris.Barnes.2000@me.com, subject: 'The Pipeline failed :( \n${env.BUILD_ID} on ${env.JENKINS_URL}'
        }
    }
}
