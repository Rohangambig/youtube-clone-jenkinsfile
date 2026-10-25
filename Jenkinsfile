pipeline {
    agent {
        node {
            label "AGENT1"
        }
    }


    stages {

        stage('GIT Checkout') {
            steps {
                git(
                    branch: "${BRANCH}",
                    credentialsId: 'GITHUB',
                    url: 'https://github.com/Rohangambig/kube-system-user-service'
                )
            }
        }

    
        stage('Build and Push Image') {
            steps {
                script {
                    def timestamp = sh(
                        script: 'date +%Y%m%d%H%M%S',
                        returnStdout: true
                    ).trim()
        
                    def imageTag = "${env.BUILD_NUMBER}-${timestamp}"
                    def imageName = "rohanambig/youtube-user-service:${imageTag}"
        
                    echo "Building image: ${imageName}"
        
                    // Build Docker image
                    sh "docker build -t ${imageName} ."
        
                    // Login and push Docker image
                    withCredentials([
                        usernamePassword(
                            credentialsId: 'DOCKER',
                            usernameVariable: 'DOCKER_USERNAME',
                            passwordVariable: 'DOCKER_PASSWORD'
                        )
                    ]) {
                        sh '''
                            set +x
                            echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        '''
        
                        sh "docker push ${imageName}"
        
                        sh 'docker logout'
                    }
                }
            }
        }

        
    }
}
