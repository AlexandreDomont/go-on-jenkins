pipeline {
	agent any
 	environment {
        	GO111MODULE = 'auto'
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
