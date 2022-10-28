pipeline {
    agent { label 'tuto' }
    
    environment {
        DOCKERHUB_CREDS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Build') {
            steps {
                container('podman') {
                    script {
                        sh 'podman build -t  dockerhub.io/leariel98/web-go:$BUILD_NUMBER -f Dockerfile'
                        sh 'podman login docker.io -u $DOCKERHUB_CREDS_USR -p $DOCKERHUB_CREDS_PSW'
                        sh 'podman push docker.io/leariel98/web-go:$BUILD_NUMBER'
                    }
                }
            }
        }
    }
}
