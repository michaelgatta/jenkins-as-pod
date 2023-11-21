pipeline {
    agent {
        mike {
            // Your Kubernetes configuration here
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
  name: jenkins-agent
spec:
  containers:
  - name: maven
    image: maven:3.8.4
    command:
    - cat
    tty: true
"""
        }
    }

    stages {
        stage('Build') {
            steps {
                container('maven') {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Test') {
            steps {
                container('maven') {
                    sh 'mvn test'
                }
            }
        }

        stage('Deploy') {
            steps {
                container('maven') {
                    sh 'mvn deploy'
                }
            }
        }
    }
}
