pipeline { 
    agent { label "slave-01"}
    
    tools {
        maven 'maven3'
        jdk 'jdk17'
    }
    environment{
 SCANNER_HOME= tool 'sonar-scanner'
 }

    

    stages {
        
        stage('Compile') {
            steps {
            sh  "mvn compile"
            }
        }
        
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }

        
        stage('Package') {
            steps {
                sh "mvn package"
            }
        }


        stage('SonarQube Analysis') {
            steps {
            withSonarQubeEnv('sonar-server') {

            sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=bloggingApp \
            -Dsonar.projectKey=bloggingApp \
            -Dsonar.java.binaries=target'''


            }
            }
            }
            stage('Quilty Gate Check') {
            steps {
                timeout(time: 1, unit: 'HOURS') {

                  waitForQualityGate abortPipeline: false, credentialsId: 'sonar-secret'
                }
            }
            }

    }
}
