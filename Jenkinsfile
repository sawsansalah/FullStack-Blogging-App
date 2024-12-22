pipeline { 
    agent any
    
    tools {
        maven 'maven3'
        jdk 'jdk17'
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

            sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=bloggingApp -
            Dsonar.projectKey=bloggingApp \
            -Dsonar.java.binaries=target -Dsonar.branch.name=main'''

            sh "echo $SCANNER_HOME"

            }
            }
            }

    }
}
