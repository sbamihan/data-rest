pipeline {
	agent none
	stages {
		agent { docker 'maven:3-alpine' }
		stage('Clone repository') {
			git 'https://github.com/sbamihan/data-rest.git'
		}
		
		stage('Build Jar') {
			steps {
				sh 'mvn package'
			}
		}
	}
}
