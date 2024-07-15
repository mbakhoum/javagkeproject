pipeline {
    agent any
    environment {
        PROJECT_ID = 'cicd-javaapp'
        CLUSTER_NAME = 'javacluster'
        ZONE = 'us-central1-c'
        APP_NAME = 'test'
        CONTAINER_NAME = 'dockertest'
        IMAGE_TAG = "latest"
    }
    stages {
        stage('Deploy to GKE') {
            steps {
                script {
                    withCredentials([gcpServiceAccount(credentialsId: 'jenkinstokengke', project: "${PROJECT_ID}")]) {
                        sh "gcloud container clusters get-credentials ${CLUSTER_NAME} --zone ${ZONE} --project ${PROJECT_ID}"
                        sh "kubectl set image deployment/${APP_NAME} ${CONTAINER_NAME}=gcr.io/${PROJECT_ID}/${CONTAINER_NAME}:${IMAGE_TAG}"
                    }
                }
            }
        }
    }
