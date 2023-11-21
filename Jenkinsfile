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
            stage('git clone'){
                steps{
                    sh "echo love"
                }
            }
            stage('heaven'){
                steps{
                    sh "echo mike"
                }
            }
        }
    
}