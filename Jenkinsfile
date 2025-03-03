pipeline {
  agent any
  tools {
  nodejs 'NodeJS'
  dockerTool 'docker_latest'
}
  stages{
    stage('VM Node Version'){
      input {
                message "Should we continue?"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }     
      steps{
           sh '''
                 node -v 
                 npm -v
                 echo "hello $PERSON"
                 docker --version
              '''
      }
    }
  }
}