pipeline {
	agent { docker 'maven:3-alpine' }
	
	stages {
		stage('Clone repository') {
			git 'https://github.com/sbamihan/data-rest.git'
		}
	}
	
	stages {
		stage('Build Jar') {
			steps {
				sh 'mvn package'
			}
		}
	}
}
