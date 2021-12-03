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
                    sh 'ssh -o StrictHostKeyChecking=no user@hostname.com uptime'
                    sh 'ssh -v user@hostname.com'
                    sh 'scp ./source/filename user@hostname.com:/remotehost/target'
                }
            }
        }
    }
}
