pipeline{
    agent {
		kubernetes {
			inheritFrom 'jenkins-agent'
			idleMinutes 5
			yamlFile 'build-pod.yaml'
			defaultContainer 'custom-agent'
		}
	}

    environment {
        AWS_ACCOUNT_ID='581426944935'
        AWS_DEFAULT_REGION = 'us-east-1'
        AWS_CREDENTIALS = credentials('aws-auth')
        IMAGE_REPO_NAME='mike00000'
        IMAGE_TAG='latest'
        REPOSITORY_URL="${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
        // PATH = "${PATH}:${getTerraformPath()}"
    }

    stages{
        stage('authen'){
            steps{
                script {
    withCredentials([usernamePassword(credentialsId: 'aws-auth', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
        sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 581426944935.dkr.ecr.us-east-1.amazonaws.com"
    }
}

            }
        }

        stage('docker build'){
            steps{
                script{
                    sh "docker build -t mike00000 ."
                }
            }

            stage('push'){
                steps{
                    script{
                    sh "docker tag mike00000:latest 581426944935.dkr.ecr.us-east-1.amazonaws.com/mike00000:latest"
                    sh "docker push 581426944935.dkr.ecr.us-east-1.amazonaws.com/mike00000:latest"
                    }
                }
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
    