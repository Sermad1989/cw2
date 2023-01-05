node{
    def app

    stage('Clone repository'){

        checkout scm
    }

    stage('Build image'){
    
        app = docker.build("salkassab89/cw2")
    }

    stage('Test image'){
   
        app.inside{
            sh 'echo "Tests passed" '
        }
    }
    
    stage('Push image'){
        
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
             apps.push("${env.BUILD_NUMBER}")
             appls.push("latest")
        }
    }
}
