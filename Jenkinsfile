pipeline {
	agent any

	stages {
	
		stage('Checkout'){
			
			git (
				branch:"${BRANCH}"
				credentialsId:'GITHUB'
				url:'https://github.com/Rohangambig/youtube-clone-ui'
			)			
			
		}	

	}
	
}
