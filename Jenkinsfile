pipeline {
  agent none
  stages{
    stage('Build Jar'){
        agent {
          docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
          }
        }
        steps {
			git 'https://github.com/sbamihan/data-rest.git'
            sh 'mvn package'
            stash includes: 'target/*.jar', name: 'targetfiles'
        }
    }
    stage('Deploy') {
        agent {
          docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
          }
        }

      steps {
            script{
                def image = docker.build("sbamihan/data-rest", ' .')
            }
      }
	  
	  post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
            success {
               junit '**/target/surefire-reports/TEST-*.xml'
               archiveArtifacts 'target/*.jar'
            }
         }
    }
  }
}
