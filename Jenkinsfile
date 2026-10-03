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

		stage("Build Image") {
			steps{
				script {
					def timestamp = sh(
               				 script: 'date +%Y%m%d%H%M%S',
              				  returnStdout: true
           				 ).trim()
	
        		    app_image = "rohanambig/youtube-ui:${BUILD_NUMBER}-${timestamp}"

					sh 'docker build -t ${app_image} .'
				}
			}
		}

		stage('Push Image') {
			steps {
				withCredentials([
					usernamePassword(
						credentialsId: "DOCKER",
						usernameVariable: "DOCKER_USERNAME",
						passwordVariable: "DOCKER_PASSWORD"
					)
				]) {

					sh """ 

						echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin
						docker push ${app_image}
						docker logout

					"""

				}
			}
		}
	
	}
	
}
