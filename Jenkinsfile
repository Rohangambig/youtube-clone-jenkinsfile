pipeline {
	agent any

	stages {
	
		stage('Checkout'){
		steps {
			git (
				branch:"${BRANCH}",
				credentialsId:'GITHUB',
				url:'https://github.com/Rohangambig/youtube-clone-ui'
			)			
		}	
		}

		stage('Install') {
			steps	{
				sh 'npm install'
			}
		}

		stage('Build app'){
			
			steps {
				sh 'tsc -b && vite build'
			}			

		}	

		stage('Docker build') {
			
			steps {

				sh 'docker build -t rohanambig/youtube-ui:${BUILD_NUMBER}-$(date +%Y%m%d%H%M%S) .'
			}
			
		}

	}
	
}
