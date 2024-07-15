pipeline {
    agent any
    node {
      stage('List pods') {
        withKubeConfig([credentialsId: 'jenkinstokengke',
                    serverUrl: 'https://34.28.156.24',
                    clusterName: 'javacluster',
                    namespace: 'default'
                    ]) {
      sh 'kubectl get pods'
        }
    }
  } 
}