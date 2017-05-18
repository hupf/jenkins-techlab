properties([
    buildDiscarder(logRotator(numToKeepStr: '5')),
    pipelineTriggers([
        pollSCM('H/5 * * * *'),
        cron('@midnight')
    ])
])

timestamps() {
    timeout(time: 10, unit: 'MINUTES') {
        node(env.JOB_NAME.split('/')[0]) {
            stage('Greeting') {
               withEnv(["NVM_HOME=${tool 'nvm'}"]) {
                    sh 'nvm --version'
                    sh 'nvm install v7.0.0'
                    sh 'node --version'
                    sh 'npm --version'
                }
            }
        }
    }
}
