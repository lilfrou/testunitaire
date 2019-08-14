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
    stage('compile stage') {
             steps {
              sh "mvn clean compile" 
                 sh"mvn clean verify"
        }
    }  
         stage('test') {
            steps {
                sh "mvn clean test"     
            }   
      }  
}
}
