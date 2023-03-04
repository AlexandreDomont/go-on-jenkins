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

		stage('Test') {
		    environment {
		        CODECOV_TOKEN = credentials('CODECOV_TOKEN')
		    }
		    steps {
		        sh 'go test ./... -coverprofile=coverage.txt'
		        sh "curl -s https://codecov.io/bash | bash -s -"
		    	}
			}		
		stage('Code Analysis') {
    			steps {
			        sh 'curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | bash -s -- -b $GOPATH/bin v1.17.1'
			        sh 'golangci-lint run'
			    }
			}		
		}
}
