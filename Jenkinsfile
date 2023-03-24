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
                sourceFiles: 'mongo/, mysql/, postgres/, Ansiblefile.yaml',
                remoteDirectory: 'docker/docker-database',
                execCommand : 'ansible-playbook -v -i /etc/ansible/hosts /home/Chakhree/docker/docker-database/Ansiblefile.yaml'
                )
            ]
            )
        ]
        )
      }
    }

    stage('Build mongo-container') {
      steps {
        sshPublisher(
        continueOnError: false, 
        failOnError: true,
        publishers: [
            sshPublisherDesc(
            configName: 'Docker',
            verbose : true,
            transfers: [
                sshTransfer(
                execCommand : 'cd /home/Chakhree/docker/docker-database/mongo; docker-compose up -d;'
                )
            ]
            )
        ]
        )
      }
    }

    stage('Build mysql-container') {
      steps {
        sshPublisher(
        continueOnError: false, 
        failOnError: true,
        publishers: [
            sshPublisherDesc(
            configName: 'Docker',
            verbose : true,
            transfers: [
                sshTransfer(
                execCommand : 'cd /home/Chakhree/docker/docker-database/mysql; docker-compose up -d;'
                )
            ]
            )
        ]
        )
      }
    }

    stage('Build postgres-container') {
      steps {
        sshPublisher(
        continueOnError: false, 
        failOnError: true,
        publishers: [
            sshPublisherDesc(
            configName: 'Docker',
            verbose : true,
            transfers: [
                sshTransfer(
                execCommand : 'cd /home/Chakhree/docker/docker-database/postgres; docker-compose up -d; docker ps;'
                )
            ]
            )
        ]
        )
      }
    }

  }
}
