pipeline {
    agent any
    environment {
    	CI ='true'
    }
    stages {
        stage('Build') {
            steps {
                bash 'npm install'
            }
        }
        
        stage('Test') {
            steps {
                bash 'chmod +x ./jenkins/scripts/test.sh && ./jenkins/scripts/test.sh'
            }
        }
        
        
    }
}
