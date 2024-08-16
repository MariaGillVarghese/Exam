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
        stage('Archive'){
            steps {
                archiveArtifacts artifacts: '*.jar', allowEmptyArchive: true
            }
        }
    }

}
