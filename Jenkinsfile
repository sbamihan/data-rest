pipeline {
	agent any
	stages{
		stage('Build Jar'){
			agent {
				docker {
					image 'maven:3-alpine'
					args '-v /root/.m2:/root/.m2'
				}
			}
			steps {
				sh 'mvn build package'
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
			agent any
			steps {
				withDockerRegistry([ credentialsId: "docker-hub-credentials", url: "https://index.docker.io/v1/" ]) {
					sh 'docker push sherwinamihan/data-rest:${env.BUILD_NUMBER}'
				}
			}
		}
        
	}
}
