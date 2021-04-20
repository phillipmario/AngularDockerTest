node ("build-node-linux") {
    def app
 
        stage('Clone repository') {
            checkout scm
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
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BUILD_NUMBER}")
                app.push("latest")
            }
        }
  
  stage ('trying a ting'){
    sh "kubectl get nodes"
  }
 
}
