pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Test') {
            steps {
                sh 'chmod +x ./jenkins/scripts/test.sh && ./jenkins/scripts/test.sh'
            }
        }
        
	stage('Deliver for development') {
	    when {
		branch 'development'
	    }
	    steps {
		sh './jenkins/scripts/deliver-for-development.sh'
		timeout(time: 5, unit: 'MINUTES') { // Set timeout here
		    input message: 'Finished using the web site? (Click "Proceed" to continue)'
		}
		sh './jenkins/scripts/kill.sh'
	    }
	}

	stage('Deploy for production') {
	    when {
		branch 'production'
	    }
	    steps {
		sh './jenkins/scripts/deploy-for-production.sh'
		timeout(time: 5, unit: 'MINUTES') { // Set timeout here
		    input message: 'Finished using the web site? (Click "Proceed" to continue)'
		}
		sh './jenkins/scripts/kill.sh'
	    }
	}


    }
}
