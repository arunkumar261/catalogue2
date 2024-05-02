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
        stage('Build') {
            steps {
                sh """
                    ls -la
                    zip -q -r catalogue2.zip ./* -x ".git" -x "*.zip"
                    ls -ltr

                """
            }
        }
        stage('Publish to nexus') {
            steps {
                 nexusArtifactUploader(
                 nexusVersion: 'nexus3',
                 protocol: 'http',
                 nexusUrl: "${nexusURL}",
                 groupId: 'com.roboshop',
                 version: "${packageVersion}",
                 repository: 'catalogue2',
                 credentialsId: 'nexus-auth',
                 artifacts: [
                        [artifactId: 'catalogue2',
                        classifier: '',
                        file: 'catalogue2.zip',
                        type: 'zip']
                    ]
                )
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

        stage('trigger catalogue-deploy2 pipeline') {
            steps {
                
                build job: 'catalogue-deploy2', wait: true,
                parameters: [
                    string(name: 'version', value: "${packageVersion}"),
                    string(name: 'environment', value: "dev"),
                ]
            }
        }
    }

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