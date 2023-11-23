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
    }
}

    