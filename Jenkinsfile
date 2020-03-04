pipeline {
  agent any
  stages{
	stage('Clone Repository'){
        steps {
			git 'https://github.com/sbamihan/data-rest.git'
        }
    }
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
	stage('Deploy'){
        steps {
			script{
                def image = docker.build("sbamihan/data-rest", ' .')
            }
        }
    }
  }
}
