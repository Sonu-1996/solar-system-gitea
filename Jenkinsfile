pipeline {
  agent any
  tools {
    nodejs 'NodeJS'
  }
  stages{
      stage('Installing Dependencies'){
        // input {
        //           message "Should we continue?"
        //           parameters {
        //               string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        //           }
        //       }     
        steps{
            sh 'npm install --no-audit'
            sh 'npm audit fix --force'
        }
      }
      stage('Dependency Checks') {
        parallel {
          stage('NPM Dependency Audit '){
            steps {
              script{
                try{
                    sh '''
                      npm audit --audit-level=critical
                      echo $?
                    '''
                  } 
                catch (err) {
                  echo "Caught: ${err}"
                  currentBuild.result = 'UNSTABLE'
                } 
              }   
            }
          }
          stage('OWASP Dependency Check'){  
            steps {
              dependencyCheck additionalArguments: '''
              --project \'pipeline-learn\'
              --scan \'./\'
              --format \'ALL\' 
              --prettyPrint''', odcInstallation: 'OWASP Dependency Check'

              dependencyCheckPublisher failedTotalCritical: 1, pattern: 'dependency-check-report.xml', stopBuild: true

              publishHTML([allowMissing: true, alwaysLinkToLastBuild: true, keepAll: true, reportDir: './', reportFiles: 'dependency-check-jenkins.html', reportName: 'Dependency Check HTML Report', reportTitles: '', useWrapperFileDirectly: true])
            }     
          }  
       }  
    
    }
     stage('Unit Testing') {
      steps {
        sh 'npm test'
      }
    
     }
  }  
}


