pipeline {
    agent {
        node {
            label 'Agent-1'
        }
    }

    environment {
        packageVersion = ''
    }

    options {
        timeout(time:1, unit: 'HOURS')
        disableConcurrentBuilds()
    }

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

        stage('install dependencies') {
            steps {
                sh """
                    npm install
                """
            }
        }

        stage('Test') {
            steps {
                 echo "this is testing stage"
            }
        }
        stage('Deploy') {
            steps {
                 sh """
                 echo "Here im writing shell script"
                """
            }
        }
    }

    post {
        always {
            echo "I will always say Hello"
        }
        failure {
            echo "I will say Hello only pipeline fails"
        }
        success {
            echo "I will say Hello only pipeline success"
        }
    }
}