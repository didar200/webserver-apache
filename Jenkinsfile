pipeline {
    agent any
	
    environment {
        dockerImage =''
        registry = 'didar200/webserver-apache'
        registryCredential = 'dockerhub'
    }

    stages {
        stage('Build'){
            steps{
                script{
                    dockerImage = docker.build registry
                }
            }
        }

	stage('Push') {
            steps {
                script{
                    docker.withRegistry( '', registryCredential ) {
			dockerImage.push()
		    }
                }
	    }
	}
        stage('Deploy to K8s') {
            steps {
              script {
                kubernetesDeploy (configs: 'webserver.yaml',kubeconfigId: 'kubernetes')
              }
            }
        }
    }
}
