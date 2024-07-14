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
        stage('Print Credential'){
            steps {
               echo "Building Project ${env.PROJECT_ID} ..."
               sh 'chmod +x build.sh'
               withCredentials([string(credentialsId: 'sample-credential', variable: 'API_KEY')]) {
                  sh '''
                     ./build.sh
                  '''
               }
            }
        }
        stage('Deploy to GKE') {
            steps{
                step(
                    withKubeConfig([credentialsId: env.CREDENTIALS_ID,
                    clusterName: env.CLUSTER_NAME,
                    namespace: env.NAMESPACE
                    ]) {
                   sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
                   sh 'chmod u+x ./kubectl'  
                   sh './kubectl apply -f nginx.yaml'
             
                  }
                )
            }
     }
  }
}