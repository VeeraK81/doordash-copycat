pipeline {
    agent any
    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main', url: 'https://github.com/VeeraK81/doordash-copycat.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('doordash-fee-service:latest')
                }
            }
        }
    }
    post {
        success {
            script {
                echo "Success"
                emailext(
                    subject: "Jenkins Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """<p>Good news!</p>
                             <p>The build <b>${env.JOB_NAME} #${env.BUILD_NUMBER}</b> was successful.</p>
                             <p>View the details <a href="${env.BUILD_URL}">here</a>.</p>""",
                    to: 'v.kannan@tbs-education.org'
                )
            }
        }
        failure {
            script {
                echo "Failure"
                emailext(
                    subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """<p>Unfortunately, the build <b>${env.JOB_NAME} #${env.BUILD_NUMBER}</b> has failed.</p>
                             <p>Please check the logs and address the issues.</p>
                             <p>View the details <a href="${env.BUILD_URL}">here</a>.</p>""",
                    to: 'v.kannan@tbs-education.org'
                )
            }
        }
    }
}