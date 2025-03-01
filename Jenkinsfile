pipeline {
  agent {
    docker {
      image 'ubuntu:latest'
    }

  }
  stages {
    stage('test') {
      steps {
        isunix()
      }
    }

  }
}
