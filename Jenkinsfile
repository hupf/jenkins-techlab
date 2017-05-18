pipeline {
    agent { label env.JOB_NAME.split('/')[0] }
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        timeout(time: 10, unit: 'MINUTES')
        timestamps()  // Requires the "Timestamper Plugin"
    }
    triggers {
        pollSCM('H/5 * * * *')
        cron('@midnight')
    }
    stages {
        stage('Build') {
            steps {
                withEnv(["NVM_HOME=${tool 'nvm'}"]) {
                    sh 'nvm --version'
                    sh 'nvm install v7.0.0'
                    sh 'nvm use v7.0.0'
                    sh 'node --version'
                    sh 'npm --version'
                }
            }
        }
    }
}
