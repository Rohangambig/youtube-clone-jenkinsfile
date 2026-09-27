pipeline {
	agent AGENT1

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
