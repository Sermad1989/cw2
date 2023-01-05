node{
    def app

    stage('Clone repository'){

        checkout scm
    }

    stage('Build image'){
    
        app = docker.build('salkassab89/cw2:1.0')
    }

    stage('Test image'){
   
        app.inside{
            sh 'echo "Tests passed" '
        }
    }
    
    stage('Push image'){
        
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
        }
    }
    stage('Deploy image'){
        sshagent(['my-ssh-key']) {
             sh 'curl 10.104.150.27:30930'
             sh 'kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v3'
        }
    }
}
