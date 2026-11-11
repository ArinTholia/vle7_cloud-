pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'arintholia'
        APP_NAME = 'vle7-app'
        IMAGE_NAME = "${DOCKER_REGISTRY}/${APP_NAME}:latest"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh "kubectl apply -f k8s/deployment.yaml"
                sh "kubectl apply -f k8s/service.yaml"
                sh "kubectl rollout status deployment/vle7-app"
            }
        }

        stage('Verify Service') {
            steps {
                sh "kubectl get pods -l app=vle7-app"
                sh "kubectl get svc vle7-service"
            }
        }
    }
}
