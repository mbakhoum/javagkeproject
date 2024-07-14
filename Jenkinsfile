pipeline {
    agent any
    environment {
        PROJECT_ID = 'cicd-javaapp'
        CLUSTER_NAME = 'javacluster'
        LOCATION = 'us-central1-c'
        NAMESPACE = 'testpipeline'
    }
     stages {
        stage('Deploy to GKE') {
            steps{
                step([
                $class: 'KubernetesEngineBuilder',
                projectId: env.PROJECT_ID,
                clusterName: env.CLUSTER_NAME,
                location: env.LOCATION,
                manifestPattern: 'manifest.yaml',
                credentialsId: "CICD-JavaApp",
                verifyDeployments: true])
            }
        }
    }
}