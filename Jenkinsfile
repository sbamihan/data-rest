pipeline {
	agent { docker 'maven:3-alpine' }
	
	stages {
		stage('Clone repository') {
			checkout scm
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
