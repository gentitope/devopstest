pipeline {
    agent any

    stages {
        stage('checkout app repo') {
          steps {
               checkout([
                   $class: 'GitSCM',
                   branches: [[name: "main"]],
                   doGenerateSubmoduleConfigurations: false,
                   extensions: [],
                   userRemoteConfigs: [[credentialsId: 'github-jenkins-ssh', url: "git@github.com:gentitope/devopstest.git"]]
              ])
          }
        }
        stage ('Deploy') {
            steps{
                sshagent(credentials : ['github-jenkins-ssh']) {
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.16.79.249 uptime'
                    sh 'ssh -v ubuntu@172.16.79.249'
                    sh 'scp ./index.html ubuntu@172.16.79.249:/var/www/devopstest/'
                }
            }
        }
    }
}
