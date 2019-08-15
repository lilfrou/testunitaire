pipeline {
    agent any
stages {
        stage("clone code") {
            steps {
                script {
                    // Let's clone the source
                    git 'https://github.com/lilfrou/testunitaire.git';
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
      }  
    stage('sonar') {
         steps{
    sh 'mvn -X clean verify sonar:sonar\
  -Dsonar.projectKey=lilfrou_testunitaire \
  -Dsonar.organization=lilfrou-github \
  -Dsonar.host.url=https://sonarcloud.io \
  -Dsonar.login=e189365c4558258b652641977ce8374c17e0805f\
  -Dsonar.java.libraries=target'
    }     
}  
}
}
