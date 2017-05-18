//@Library('jenkins-techlab-libraries') _

pipeline {
    agent { label env.JOB_NAME.split('/')[0] }
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        timeout(time: 10, unit: 'MINUTES')
        timestamps()  // Timestamper Plugin
        ansiColor('xterm')  // AnsiColor Plugin
    }
    triggers {
        pollSCM('H/5 * * * *')
    }
    environment {
        NVM_HOME = tool('nvm')
    }
    stages {
        stage('Build') {
            steps {
                sh """#!/bin/bash +x
                    source \${HOME}/.nvm/nvm.sh
                    nvm install 7
                    npm install
                    npm test
                """
            }
            post {
                always {
                    //archiveArtifacts 'junit/*.xml'
                    junit 'junit/*.xml'
                }
            }
        }
    }
    post {
        success {
            mail subject: 'Success', body: "Build success - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", to: 'hofer@puzzle.ch'
        }
        unstable {
            mail subject: 'Unstable', body: "Build unstable - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", to: 'hofer@puzzle.ch'
        }
        failure {
            mail subject: 'Failure', body: "Build failure - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", to: 'hofer@puzzle.ch'
        }
    }
}
