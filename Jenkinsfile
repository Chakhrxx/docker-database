pipeline {
  agent any

  stages {

    stage('SSH Tranfer and run Ansivle playbook') {
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
                remoteDirectory: 'docker/docker-database',
                execCommand : 'ansible-playbook -v -i /etc/ansible/hosts /home/Chakhree/docker/docker-database/Ansiblefile.yaml'
                )
            ]
            )
        ]
        )
      }
    }

    stage('Build cassandra container') {
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
                execCommand : 'docker stop cassandra-container; docker rm cassandra-container; docker-compose -f /home/Chakhree/docker/docker-database/cassandra/docker-compose.yaml up -d'
                )
            ]
            )
        ]
        )
      }
    }

    stage('Build mongo container') {
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
                execCommand : 'docker stop mongo-container; docker rm mongo-container; docker-compose -f /home/Chakhree/docker/docker-database/mongo/docker-compose.yaml up -d'
                )
            ]
            )
        ]
        )
      }
    }

    stage('Build mysql container') {
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
                execCommand : 'docker stop mysql-container; docker rm mysql-container; docker-compose -f /home/Chakhree/docker/docker-database/mysql/docker-compose.yaml up -d'
                )
            ]
            )
        ]
        )
      }
    }

    stage('Build postgres container') {
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
                execCommand : 'docker stop postgres-container; docker rm postgres-container; docker-compose /home/Chakhree/docker/docker-database/postgres/docker-compose.yaml up -d'
                )
            ]
            )
        ]
        )
      }
    }

  }
}
