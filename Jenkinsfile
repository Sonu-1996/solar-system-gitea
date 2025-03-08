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
        }
      }

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
            currentBuild.result = 'SUCCESS'
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
      }

    }
  }
}


