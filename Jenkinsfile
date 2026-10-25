pipeline {
    agent {
        node {
            label "AGENT1"
        }
    }

    environment {
        APP_IMAGE = ''
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

            stage('Build Image') {
                steps {
                    script {
                        def timestamp = sh(
                            script: 'date +%Y%m%d%H%M%S',
                            returnStdout: true
                        ).trim()
            
                        env.APP_IMAGE = "rohanambig/youtube-user-service:${env.BUILD_NUMBER}-${timestamp}"
            
                        echo "Docker image: ${env.APP_IMAGE}"
            
                        sh 'docker build -t "$APP_IMAGE" .'
                    }
                }
            }

        stage('Push Image') {
            steps {
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
                        docker push "$APP_IMAGE"
                        docker logout
                    '''
                }
            }
        }
    }
}
