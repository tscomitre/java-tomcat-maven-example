pipeline {

    agent any
    stages {

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
    }
}