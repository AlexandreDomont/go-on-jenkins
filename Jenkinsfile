pipeline {
	agent any
 	environment {
        	GO111MODULE = 'auto'
		py2Ana="0"	
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
		            echo "Find Anaconda2 Python installation.."
	                    py2Ana=`git tag --contains`
			    echo \$py2Ana	
	        	"""
			 //script {  env.py2Ana = sh (script: 'sh date', , returnStdout:true).trim()	}	
			script {
				def TAG_NAME = sh(returnStdout: true, script: "git tag --contains").trim() 
				if (TAG_NAME != null) {
				sh "echo $TAG_NAME"
				} else {
				 sh "echo Non-tag build"
				}}
			}
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
				echo "${env.py2Ana}"
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
