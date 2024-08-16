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
            // Catch errors in the test step and mark the build as UNSTABLE if any occur
            catchError(buildResult: 'UNSTABLE', stageResult: 'UNSTABLE', message: 'Test Failed') {
                // Run the Maven tests
                sh "mvn test"
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
