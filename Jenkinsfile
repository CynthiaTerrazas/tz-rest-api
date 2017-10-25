pipeline {
    agent any

    stages {
        stage('Commit') {
            steps {
               sh './gradlew clean assemble'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew clean check'
                publishHTML target: [
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                keepAll: true,
                reportDir: 'build/reports/tests/test/',
                reportFiles: 'index.html',
                reportName: 'Jenkins Unit test Reports'
              ]
            }
        }
        stage('Package') {
            steps {
                sh './gradlew shadowJar'
            }
        }
    }
}