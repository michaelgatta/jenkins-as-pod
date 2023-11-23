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
					      withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'jenkins-kubernetes-credential', namespace: '', restrictKubeConfigAccess: false, serverUrl: 'https://api-onyxquity-pi-k8s-loca-lomnoc-3b8bb5f5312891d0.elb.us-east-1.amazonaws.com') {
						//   sh returnStatus: true, script: 'kubectl create secret docker-registry regcred --docker-server=${REGISTRY_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com --docker-username=AWS --docker-password=$(aws ecr get-login-password)'
						  sh 'kubectl apply -f k8sbook.yaml'
						 // sh 'envsubst < kjavaapps.yaml | kubectl apply -f -'
					}
                }
            
    }

        
    }
    
}
}
    