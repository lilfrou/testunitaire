pipeline {
   
    agent any
stages {
        stage("clone code") {
            steps {
                script {
                    // Let's clone the source
                    git 'https://github.com/lilfrou/testunitaire.git',branch: 'master';
                }
            }
        }
    stage('clean stage') {
             steps {
              sh "mvn clean" 
                 
        }
    }  
         stage('test') {
            steps {
                sh "mvn test" 
                
          
           }
             post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
    }
      }  
    
    stage('sonar') {
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
     stage("speak") {
         steps{
        slackSend color: '#BADA55', message: '##################################################'
        slackSend color: '#BADA55', message: '###########****ALL STAGES COMPLETED****#############'
        slackSend color: '#BADA55', message: '##################################################'
    }

}
}
} 
