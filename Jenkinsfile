def casee ="true"
pipeline {
   
    agent any
   
stages {
   
      
    stage('clean stage') {
             steps {
                 catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
              sh "mvn clean" 
                 
        }
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
               casee ="false" }
                
                }
            }
      }  
         stage("false")
   {
      steps{
         script{
            casee="false"}
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
  -Dsonar.branch.name=develop\
  -Dsonar.pullrequest.target=master\
  -Dsonar.java.libraries=target'
     
         } 
         }
     stage('sonarpull23') {
      when {
                branch 'master'
            }
        
         steps{
            script{
    sh 'mvn -X clean verify sonar:sonar\
             -Dsonar.projectKey=lilfrou_testunitaire \
  -Dsonar.organization=lilfrou-github \
  -Dsonar.host.url=https://sonarcloud.io \
  -Dsonar.login=e189365c4558258b652641977ce8374c17e0805f\
             -Dsonar.pullrequest.key=4\
  -Dsonar.pullrequest.branch=feature/develop\
  -Dsonar.pullrequest.base=master\
  -Dsonar.java.libraries=target'
               casee="false"
            }
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
               
               script{
                  
                  if(casee =="true")
                  {
                     cleanWs() }
                  else { echo 'I execute elsewhere'}
               }
               }
            }
     
}
} 
