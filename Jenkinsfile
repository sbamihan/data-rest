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
					def image = docker.build("sbamihan/data-rest", ' .')
				}
			}
		}
		stage('Docker Push') {
			agent any
			steps {
				withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: '6k0Nv1naP', usernameVariable: 'sherwinamihan')]) {
					sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
					sh 'docker push sbamihan/data-rest:latest'
				}
			}
		}
	}
}
