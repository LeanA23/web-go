pipeline {
    agent { label 'tuto' }
    
    environment {
        DOCKERHUB_CREDS = credentials("dockerhub-credentials")
    }

    stages {
        stage('Build') {
            steps {
                container('podman') {
                    script {
                        sh 'podman build -t  dockerhub.io/leariel98/web-go:$BUILD_NUMBER -f Dockerfile'
                        sh 'podman login -u $DOCKERHUB_CREDS_USR -p DOCKERHUB_CREDS_PSW'
                        sh 'podman push docker.io/leariel98/web-go:$BUILD_NUMBER'
                    }
                }
                container('kubectl') {
                    script {
                        sh 'env'
                        sh 'kubectl get pods'
                    }
                }
                container('fortune') {
                    script {
                        sh 'fortune'
                    }
                }
            }
        }
    }
}
