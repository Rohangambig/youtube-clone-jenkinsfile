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

                    // Explicitly update the global env variable
                    env.APP_IMAGE = "rohanambig/youtube-user-service:${BUILD_NUMBER}-${timestamp}"

                    sh "docker build -t ${env.APP_IMAGE} ."
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
                    // Use double quotes (""") so Groovy interpolates ${env.APP_IMAGE}
                    sh """
                        set +x
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker push "${env.APP_IMAGE}"
                        docker logout
                    """
                }
            }
        }
    }
}
