pipeline {
  agent {
    node {
      label 'agent1'
    }

  }
  stages {
    stage('Clone') {
      steps {
        git(url: 'https://github.com/shyamsharma23/restapi-1.0', branch: 'api', poll: true)
      }
    }

    stage('Build') {
      steps {
        echo 'Building'
        sh 'mvn -Dmaven.test.failure.ignore=true clean package'
        tool 'M3'
      }
    }

    stage('Package') {
      agent {
        node {
          label 'agent1'
        }

      }
      steps {
        echo 'Deployed'
        archiveArtifacts(artifacts: 'target/*.jar', allowEmptyArchive: true)
      }
    }

    stage('Deploy') {
      steps {
        sh '''cd target
java -jar demo-0.0.1-SNAPSHOT.jar'''
      }
    }

  }
}