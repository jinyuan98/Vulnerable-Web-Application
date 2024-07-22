pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/jinyuan98/Vulnerable-Web-Application.git'
            }
        }

        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube'
                    withSonarQubeEnv('SonarQube') {
                        sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=OWASP \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://172.17.0.2:9000 \
                        -X
                        """
                    }
                }
            }
        }
    }
    post {
        always {
            script {
                junit testResults: '**/target/surefire-reports/TEST-*.xml'
                recordIssues enabledForFailure: true, tool: sonarQube()
            }
        }
    }
}
