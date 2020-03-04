pipeline {
	agent none
	stages {
		stage('Clone repository') {
			checkout scm
		}
	}
	
	agent { docker 'maven:3-alpine' }
	stages {
		stage('Build Jar') {
			steps {
				sh 'mvn package'
			}
		}
	}
}
