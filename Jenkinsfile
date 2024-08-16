pipeline {
    agent {
        label 'agent'
    }

    stages {
        stage('Build') {
            steps {
                sh 'which mvn'          // Check if Maven is installed
                sh 'mvn --version'
                checkout scm
                sh "mvn package"
            }
        }
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }
        stage('Code Coverage') {
            steps {
                sh "mvn jacoco:report"
            }
        }
        stage('Archive'){
            steps {
                archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
            }
        }
    }

}
