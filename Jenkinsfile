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
             sshagent (['my-ssh-key']){
             sh 'ssh ubuntu@3.80.101.112
             docker pull salkassab89/cw2:1.0
             kubectl set image deployments/kubernetes-bootcamp cw2=jocatalin/kubernetes-bootcamp:v2'
             }

    }

}
