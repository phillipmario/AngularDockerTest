node {
    def app

    agent none
    
    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
     agent { label "angular" }  
     app = docker.build("phillipmario/test")
    }

    stage('Test image') {
      agent { label "angular" }
        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
     agent { label "angular" }
        docker.withRegistry('https://registry.hub.docker.com', 'Docker') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
