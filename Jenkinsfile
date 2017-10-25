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

        stage('CodeQuality') {

            steps {
                sh './gradlew sonarqube -Dsonar.host.url=http://sonarqube:9000'
                sh './gradlew jacocoTestReport'
                publishHTML target: [
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                keepAll: true,
                reportDir: 'build/jacocoHtml/',
                reportFiles: 'index.html',
                reportName: 'Jenkins coverage report'
              ]
            }

        }
        stage('Package') {
            steps {
                sh './gradlew shadowJar'
                archiveArtifacts 'build/libs/*.jar'
                archiveArtifacts 'example.yml'
            }
        }
    }
}