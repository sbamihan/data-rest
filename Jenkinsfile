pipeline {
  agent any
  stages{
	stage('Clone Repository'){
        steps {
			git 'https://github.com/sbamihan/data-rest.git'
        }
    }
	stage('Build Jar'){
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
