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
                withEnv(["NVM_DIR=${tool 'nvm'}"]) {
                    sh '''#!/bin/bash
                    source $NVM_HOME/nvm.sh
                    nvm --version
                    nvm install 7
                    nvm use 7
                    node --version
                    npm --version'''
                }
            }
        }
    }
}
