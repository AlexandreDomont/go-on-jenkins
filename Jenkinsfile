pipeline {
	agent any
 	environment {
        	GO111MODULE = 'on'
    	}	
	tools {
		go 'go-1.20.1'
	}
	stages {
		stage('Build') {
			steps {
				sh 'go build'
				}
			}			

		}
}
