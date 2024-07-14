pipeline {
    agent any
    environment {
        PROJECT_ID = 'testpipelinebuild'
        CLUSTER_NAME = 'javacluster'
        LOCATION = 'us-central1-c'
        CREDENTIALS_ID = 'jenkinstokengke'
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
                credentialsId: env.CREDENTIALS_ID,
                verifyDeployments: true])
            }
        }
    }
}