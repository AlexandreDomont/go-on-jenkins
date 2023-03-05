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
	/*	stage('Code Analysis') {
    			steps {
				sh 'ls -lat'
			        sh 'curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin'
			 	sh 'ls -lat'	
			        sh 'golangci-lint run'
			    }
			}	*/

		stage ('Get TAG')
		{
			
			steps {
			sh """
		            echo Find Anaconda2 Python installation...
	                    py2Ana=`which -a python | grep --max-count=1 anaconda2`        		    
			    git tag --contains
	        	"""	}
		}

		stage ('echo')
		{
			environment { 
				TAG_NAME="1" 
				TITI="1" 
				TOTO = 1
				}	

			steps {
				echo "rien"
				}


		}

		/*stage('Release') {
		   environment {
			GITHUB_TOKEN = credentials('GITHUB_TOKEN')
			}
 		   when {
		        buildingTag()
    			}
		    steps {
		        sh 'curl -sL https://git.io/goreleaser | bash'
		    }	
	
		} */	
		}
}
