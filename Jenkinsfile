pipeline {
  agent any
  tools {
  nodejs 'NodeJS'
}
  stages{
    stage('VM Node Version'){
      steps{
           sh '''
                 node -v 
                 npm -v
              '''
      }
    }
  }
}