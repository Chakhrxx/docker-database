pipeline {
    agent any

    stages {
        stage('Connect to remote host') {
            steps {
                sshagent(credentials: ['fa1b7358-d54a-4d15-a66f-124314b0be7e']) {
                    sh 'chmod 400 react_jenkins_ansible.pem'
                    sh 'ssh -i "react_jenkins_ansible.pem" ec2-user@ec2-43-207-48-197.ap-northeast-1.compute.amazonaws.com'
                    sh 'sudo su -'
                }
            }
        }
    }
}





