parameters([
    string(name: 'company_parameter', defaultValue: 'puzzle', description: 'The company the pipeline runs in')
])

node {
    stage('Build') {
        sh "echo \"Running ${env.BUILD_ID} on ${env.JENKINS_URL}\" in company ${params.company_parameter}"
    }
}
