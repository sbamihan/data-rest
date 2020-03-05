pipeline {
	agent any
	stages{
		stage('Build Artifact'){
			steps {
				sh 'mvn package'
				stash includes: 'target/*.jar', name: 'targetfiles'
			}
		}
		
		stage('Build Image'){
			steps {
				script{
					def image = docker.build("sherwinamihan/data-rest", ' .')
				}
			}
		}
		
		stage('Push Image') {
			steps {
				withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
					sh 'docker push sherwinamihan/data-rest:latest'
				}
			}
		}
	}
}
