
pipeline {

    agent any

    options {
        timestamps()
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                echo 'Building Spring Boot backend'

                dir('backend') {
                    sh './mvnw -B clean verify'
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving generated JAR'

                archiveArtifacts(
                    artifacts: 'backend/target/*.jar',
                    fingerprint: true
                )
            }
        }
    }

    post {
        success {
            echo 'Backend pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
