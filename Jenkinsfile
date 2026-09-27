pipeline {
	agent {
		node {
			label "AGENT1"
		}
	}

	stages {
	
		stage('GIT Checkout'){
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
