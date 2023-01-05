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
             sh 'docker pull salkassab89/cw2:1.0'
        }
        
        sshagent(['my-ssh-key']) {
             sh 'ansible-playbook update_version.yml'
        }

    }
}
