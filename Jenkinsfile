pipeline {
    agent {
        label 'agent'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                script {
                    catchError(buildResult: 'UNSTABLE', message: 'Tests failed') {
                        sh 'mvn test'
                    }
                }
            }
        }

        stage('Publish Test Results') {
            steps {
                junit '*/target/surefire-reports/.xml'
            }
        }

        stage('Publish Code Coverage') {
            steps {
                jacoco execPattern: '*/target/jacoco.exec', classPattern: '/target/classes', sourcePattern: '/src/main/java', exclusionPattern: '*/target/test-classes'
            }
        }

        stage('Archive the build artifacts') {
            steps {
                archiveArtifacts artifacts: '*/.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            echo 'Build completed.'
        }
    }
}