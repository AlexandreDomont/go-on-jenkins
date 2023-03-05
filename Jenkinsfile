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
				sh 'ls -lat'
			        sh 'curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin'
			 	sh 'ls -lat'	
			        sh 'golangci-lint run'
			    }
			}	

		stage ('echo')
		{
			environment { TAG_NAME="1" }	
			steps {
				echo "1 : $env.TAG_NAME " 
				sh 'git tag --contains'
				sh 'export TOTO'
				sh 'TOTO = $(git tag --contains) && echo $TOTO'

				script  {
         				env.TOTO = sh(script: 'git tag --points-at HEAD', returnStdout: true,).trim() 
					echo "$env.TOTO"
					//echo "sh(script: 'git tag --points-at HEAD', returnStdout: true,).trim()"
					//echo "sh(script: 'git tag --contains', returnStdout: true,).trim()"	
        				}
				//echo "$env.TAG_NAME"
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
