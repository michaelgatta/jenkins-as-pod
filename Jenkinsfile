pipeline{
    agent {
		kubernetes {
			inheritFrom 'jenkins-agent'
			idleMinutes 5
			yamlFile 'build-pod.yaml'
			defaultContainer 'custom-agent'
		}
	}

    stages{
        stage('welcome'){
            steps{
                sh "echo love"
            }
        }

             stage("k8s Deployment"){
			      steps {
				       script {
					      withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'jen-crd', namespace: '', restrictKubeConfigAccess: false, serverUrl: 'https://api-raycoy-new-kops-k8s-l-qhsifq-3de0f8714e553ee8.elb.us-east-1.amazonaws.com') {
						//   sh returnStatus: true, script: 'kubectl create secret docker-registry regcred --docker-server=${REGISTRY_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com --docker-username=AWS --docker-password=$(aws ecr get-login-password)'
						  sh 'kubectl apply -f k8sbook.yaml'
						 // sh 'envsubst < kjavaapps.yaml | kubectl apply -f -'
					}
                }
            
    }

        
    }
    
}
}
    