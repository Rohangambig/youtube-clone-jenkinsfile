pipeline {
	agent any

	stages {
	
		stage('Checkout'){
			steps {
				git (
					branch:"${BRANCH}",
					credentialsId:'GITHUB',
					url:'https://github.com/Rohangambig/kube-system-user-service'
				)			
			}	
		}
	
	}
	
}
