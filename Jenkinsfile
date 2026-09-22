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
				sh 'npm run build'
			}			

		}	

		stage('Docker build') {
		    steps {
       			 script {
           			 def timestamp = sh(
               				 script: 'date +%Y%m%d%H%M%S',
              				  returnStdout: true
           				 ).trim()
	
        		    app_image = "rohanambig/youtube-ui:${BUILD_NUMBER}-${timestamp}"

           		 sh "docker build -t ${app_image} ."
       				 }
 	   		}
		}

		stage('Pushing image to registry'){
			steps {
				withCredentials([
					usernamePassword(
						credentialsId:'DOCKER',
						usernameVariable:'DOCKER_USERNAME',
						passwordVariable:'DOCKER_PASSWORD'
					)
				]) {
				
					sh """
						echo "$DOCKER_PASSWORD" | docker login \
            							-u "$DOCKER_USERNAME" \
            								--password-stdin

       							 docker push "$app_image"	

        					docker logout
					"""		
		
				}
			}
		}

	}
	
}
