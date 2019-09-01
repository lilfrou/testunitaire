def casee ="true"
pipeline {
   
    agent any
   
stages {
   
      
    stage('clean stage') {
             steps {
                
                 catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
        slackSend (color: '#FFFF00', message: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")

              sh "mvn clean install -DskipTests" 
                 
        }
    }  
    }
    stage('Parallel In Sequential') {
                    parallel {
         stage('test') {
            when {
                branch 'master'
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
  -Dsonar.login=17701039889eecb892ffab60e80097a8f57449bf\
  -Dsonar.java.libraries=target'
     
         } 
         }
   stage('sonar branche') {
        when {
                branch 'master'
            }
      
         steps{
            
            
    sh 'mvn -X clean verify sonar:sonar\
  -Dsonar.projectKey=lilfrou_testunitaire \
  -Dsonar.organization=lilfrou-github \
  -Dsonar.host.url=https://sonarcloud.io \
  -Dsonar.login=17701039889eecb892ffab60e80097a8f57449bf\
  -Dsonar.branch.name=develop\
  -Dsonar.branch.name=test\
  -Dsonar.branch.target=master\
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
             -Dsonar.pullrequest.key=5\
  -Dsonar.pullrequest.branch=develop\
  -Dsonar.pullrequest.base=master\
  -Dsonar.pullrequest.provider=GitHub\
  -Dsonar.pullrequest.github.repository=lilfrou/testunitaire\
  -Dsonar.java.libraries=target'
               casee="false"
            }
    }    
}  


    
     stage("speak") {
        when {
                branch 'master'
            }
         steps{
        slackSend (color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
        slackSend color: '#BADA55', message: '##################################################'
        slackSend color: '#BADA55', message: '###########****ALL STAGES COMPLETED****#############'
        slackSend color: '#BADA55', message: '##################################################'
    }
       
     }  
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
