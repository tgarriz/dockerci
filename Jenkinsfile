pipeline {
	environment {
		registry = "https://hub.docker.com/repository/docker/tgarriz/dockerci"
		registryCredential = 'dockerhub_id'
		dockerImage = ''
	}
	agent any
	stages {
		stage('Cloning our Git') {
			steps {
				git 'https://github.com/tgarriz/dockerci.git'
			}
		}
		stage('Building our image') {
			steps{
				script {
					dockerImage = docker.build registry + ":$BUILD_NUMBER"
				}
			}
		}
		stage('Deploy our image') {
			steps{
				script {
					docker.withRegistry( '', registryCredential ) {
					dockerImage.push()
					}
				}
			}
		}
		stage('Cleaning up') {
			steps{
				sh "docker rmi $registry:$BUILD_NUMBER"
			}
		}
	}
}
