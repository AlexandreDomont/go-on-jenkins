pipeline {
	agent any
 	environment {
        	GO111MODULE = 'auto'
		py2Ana="0"	
		TAG_NAME="1"
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
			sh 'go test ./...'

//		        sh 'go test ./... -coverprofile=coverage.txt'
//		        sh "curl -s https://codecov.io/bash | bash -s -"
		    	}
			}		
	/*	stage('Code Analysis') {
    			steps {
				sh 'ls -lat'
			        sh 'curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin'
			 	sh 'ls -lat'	
			        sh 'golangci-lint run'
			    }
			}	
*/

		stage ('Get TAG')
		{
				
			
			steps {
			// DECLARATIVE 
			sh """
		            echo "Find Anaconda2 Python installation.."
	                    py2Ana=`git tag --contains`
			    echo \$py2Ana	
	        	"""
			// SCRIPTED
			script {
				TAG_NAME = sh(returnStdout: true, script: "git tag --contains").trim() 
				if (TAG_NAME != '') {
				sh "echo $TAG_NAME"
				} else {
				 sh "echo Non-tag build"
				TAG_NAME = "0"	
				}}
			}
		}

		stage ('echo TAG')
		{

			steps {
				//echo "${env.TAG_NAME}"
				echo "N° du TAG : $TAG_NAME"
				}


		}

		stage('Release') {

		   environment {GITHUB_TOKEN = credentials('GITHUB_TOKEN') }

		   when {not{expression { TAG_NAME == '0' } }}

  		   steps {  
			//sh 'git add .' 
			sh 'curl -sfL https://goreleaser.com/static/run | bash'
			}	
	
		} 	
		}
}
