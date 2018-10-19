pipeline {

    agent any
    stages {

        stage ('Cleanup') {
            cleanWs externalDelete: 'rm -rf *'
        }

        stage ('Build Servlet Project') {
            steps {
                sh '/var/jenkins_home/apache-maven-3.5.4/bin/mvn clean package'
            }

            post {
                success {
                    echo 'Now Archiving ...'
                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }

        stage ('Deploy to Staging') {
            steps {
                build job : 'Pipeline as Code - Deploy to Staging'
            }
        }

        stage ('Deploy to Production') {
            steps {
                timeout (time: 5, unit:'DAYS') {
                    input message: 'Approve PRODUCTION Deployment?'
                }

                build job : 'Pipeline as Code - Deploy to Production'
            }

            post {
                success {
                    echo 'Deployment Successful on PRODUCTION'
                }

                failure {
                    echo 'Deployment Failure on PRODUCTION'
                }
            }
        }
    }
}