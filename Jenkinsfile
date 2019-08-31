
pipeline {
   
    agent any
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'casee', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
stages {
   
      
    stage('clean stage') {
             steps {
              sh "mvn clean" 
                 
        }
    }  
         stage('test') {
            when {
                branch 'develop'
            }
                
            steps {
               script {
                  
            try { 
                
          sh "mvn test"
                 } catch (Exception e) {
               ${params.TOGGLE} ='false' }
                
                }
            }
      }  
         
    
    stage('sonar') {
       when {
                branch 'master'
            }
         steps{
            
            
    sh 'mvn -X clean verify sonar:sonar\
  -Dsonar.projectKey=lilfrou_testunitaire \
  -Dsonar.organization=lilfrou-github \
  -Dsonar.host.url=https://sonarcloud.io \
  -Dsonar.login=e189365c4558258b652641977ce8374c17e0805f\
  -Dsonar.branch.name=sonar1\
  -Dsonar.branch.name=sonar2\
  -Dsonar.branch.name=sonar3\
  -Dsonar.pullrequest.target=master\
  -Dsonar.java.libraries=target'
     
         } 
         }
  
    stage('sonarpull') {
       when {
                branch 'master'
            }
         steps{
    sh 'mvn -X clean verify sonar:sonar\
             -Dsonar.projectKey=lilfrou_testunitaire \
  -Dsonar.organization=lilfrou-github \
  -Dsonar.host.url=https://sonarcloud.io \
  -Dsonar.login=e189365c4558258b652641977ce8374c17e0805f\
             -Dsonar.pullrequest.key=2\
  -Dsonar.pullrequest.branch=feature/sonar3\
  -Dsonar.pullrequest.base=master\
  -Dsonar.java.libraries=target'
    }    
}  
     stage('sonarpull23') {
        when {
                branch 'master'
            }
        
         steps{
    sh 'mvn -X clean verify sonar:sonar\
             -Dsonar.projectKey=lilfrou_testunitaire \
  -Dsonar.organization=lilfrou-github \
  -Dsonar.host.url=https://sonarcloud.io \
  -Dsonar.login=e189365c4558258b652641977ce8374c17e0805f\
             -Dsonar.pullrequest.key=3\
  -Dsonar.pullrequest.branch=feature/sonar2\
  -Dsonar.pullrequest.base=master\
  -Dsonar.java.libraries=target'
    }    
}  

     /*stage("speak") {
        when {
                branch 'develop'
            }
         steps{
        slackSend color: '#BADA55', message: '##################################################'
        slackSend color: '#BADA55', message: '###########****ALL STAGES COMPLETED****#############'
        slackSend color: '#BADA55', message: '##################################################'
    }
       
     } */  
          stage('CleanWorkspace') {
            steps {
               
                  
                  
                  if(${params.TOGGLE} =='true')
                  {
                     cleanWs() }
                  else { echo 'I execute elsewhere'}
               }
            }
     
}
} 
