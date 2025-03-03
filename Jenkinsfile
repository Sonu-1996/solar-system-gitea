pipeline {
  agent any
  tools {
  nodejs 'NodeJS'
}
  stages{
    stage('VM Node Version'){
      input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
      steps{
           sh '''
                 node -v 
                 npm -v
              '''
      }
    }
  }
}