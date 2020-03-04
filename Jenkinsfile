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
			agent any
			steps {
				withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
					sh 'docker push sherwinamihan/data-rest:latest'
				}
			}
		}
		
		stage('Run Image') {
			agent any
			steps {
				//sh 'docker run sherwinamihan/data-rest:latest'
				script{
					docker.image('sherwinamihan/data-rest:latest').withRun('-p 8088:8080 --name data-rest') { c ->
						/* Wait until mysql service is up */
						sh 'while ! data-rest ping -h0.0.0.0 --silent; do sleep 1; done'
						/* Run some tests which require MySQL */
						sh 'echo data-rest application is running at http://localhost:8088'
					}
				}
			}
		}
	}
}
