pipeline {
 agent any
 stages {
 stage ('Checkout') {
 steps {
 git branch:'master', url: 'https://github.com/jinyuan98/Vulnerable-Web-Application.git'
 }
 }
 
 stage('Code Quality Check via SonarQube') {
 steps {
 script {
 def scannerHome = tool 'SonarQube';
 withSonarQubeEnv('SonarQube') {
 sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP1 -
Dsonar.sources=."
 }
 }
 }
 }
 }
 post {
 always {
 recordIssues enabledForFailure: true, tool: sonarQube()
 }
 }
}
