pipeline {
  agent any

  stages {

    stage('SSH Tranfer') {
      steps {
        sshPublisher(
        continueOnError: false, 
        failOnError: true,
        publishers: [
            sshPublisherDesc(
            configName: 'Ansible',
            verbose : true,
            transfers: [
                sshTransfer(
                sourceFiles: 'cassandra/, mongo/, mysql/, postgres/, Ansiblefile.yaml',
                remoteDirectory: 'docker/docker-database'
                )
            ]
            )
        ]
        )
      }
    }

    stage('Run Ansible-playbook and build Docker containers ') {
      steps {
        sshPublisher(
        continueOnError: false, 
        failOnError: true,
        publishers: [
            sshPublisherDesc(
            configName: 'Ansible',
            verbose : true,
            transfers: [
                sshTransfer(
                execCommand : 'ansible-playbook -v -i /etc/ansible/hosts /home/Chakhree/docker/docker-database/Ansiblefile.yaml'
                )
            ]
            )
        ]
        )
      }
    }


  }
}
