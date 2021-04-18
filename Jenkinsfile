node {
    def app

    agent { label "angular" }
    
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
        docker.withRegistry('https://registry.hub.docker.com', 'Docker') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
