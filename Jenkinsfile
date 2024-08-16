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
        script {
            // Execute mvn test and capture the return status
            def testStatus = sh(script: 'mvn test', returnStatus: true)
            
            // If the tests fail (exit code != 0), mark the build as UNSTABLE
            if (testStatus != 0) {
                currentBuild.result = 'UNSTABLE'
            }
        }
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
