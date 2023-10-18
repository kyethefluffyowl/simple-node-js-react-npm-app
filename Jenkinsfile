pipeline {
    agent {
        docker {
            image 'node:18.18.2-alpine3.18' 
            args '-p 3000:3000' 
        }
    }
stage('OWASP Dependency-Check Vulnerabilities') {
	      steps {
	        dependencyCheck additionalArguments: ''' 
	                    -o './'
	                    -s './'
	                    -f 'ALL' 
	                    --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities Lab06'
	        
	        dependencyCheckPublisher pattern: 'dependency-check-report.xml'
	      }
	    }
	
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
	
        // stage('Test') {
        //     steps {
        //         sh './jenkins/scripts/test.sh'
        //     }
        // }
 	stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
	
    }
}

