pipeline {
    agent {
        node {
            label 'Agent-1'
        }
    }
    environment {
        packageVersion = ''
        nexusURL = '172.31.25.31:8081'
    }

    options {
        timeout(time:1, unit: 'HOURS')
        disableConcurrentBuilds()
    }

    //  parameters {
    //     booleanParam(name: 'Deploy', defaultValue: 'false', description: 'Toggle the value')
        
    // }


    stages {
        stage('Get the version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version
                    echo "applicationversion : $packageVersion"
                }
            }
        }

        
    }
//post always executes even if success or failed
    post {
        always {
            echo "I will always say Hello"
            deleteDir()
        }
        failure {
            echo "I will say Hello only pipeline fails"
        }
        success {
            echo "I will say Hello only pipeline success"
        }
    }
}