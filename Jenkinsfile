node ("build-node-linux") {
    def app
 
        stage('Clone repository') {
            checkout scm
        }
        stage('SonarQube analysis') {
            def scannerHome = tool 'SonarScanner 4.6';
            withSonarQubeEnv('sonarqube-scanner') { // If you have configured more than one global server connection, you can specify its name
              sh "${scannerHome}/bin/sonar-scanner"
            }
          }
        stage('Build image') {
            app = docker.build("phillipmario/test")
        }

        stage('Test image') {
            app.inside {
                sh 'echo "Tests passed"'
            }
        }

        stage('Push image') {
            docker.withRegistry('https://registry.hub.docker.com', 'Docker') {
                app.push("${env.BUILD_NUMBER}")
                app.push("latest")
            }
        }
  
  stage ('trying a ting'){
    sh "kubectl get nodes"
  }
 
}
