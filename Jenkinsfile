pipeline {

    agent any
    stages {

        stage ('Build Servlet Project') {
            steps {
                sh 'export PATH=/var/jenkins_home/apache-maven-3.5.4/bin:$PATH'
                sh 'mvn clean package'
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