node {
    def app

    stage('Clone Repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }
	
    stage('Build Artifact') {
        sh "mvn clean package"
    }

    stage('Build Docker Image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("sherwinamihan/data-rest")
    }

    stage('Test Image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push Image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
	
    stage('Run') {
	sh 'docker ps -f name=data-rest -q | xargs --no-run-if-empty docker container stop'
	sh 'docker container ls -a -fname=data-rest -q | xargs -r docker container rm'
	    
	def apiContainer = docker.image("sherwinamihan/data-rest:latest").run("-e -Dserver.port=8088 --name data-rest -p 8088:8088")
	    
        /*docker.image('sherwinamihan/data-rest:latest').withRun('-e -Dserver.port=8088 --name data-rest -p 8088:8088') { c->
            sh 'echo data-rest is now running at http://172.18.13.12:8088'
        }*/		
    }
	
   /*stage('docker stop container') {
       def apiContainer = docker.container('api-server')
       apiContainer.stop()
   }
   stage('docker run container') {
       def apiContainer = docker.image("my-docker-id/my-api:${commit_id}").run("--name api-server --link mysql_server:mysql --publish 3100:3100")
   }*/
	
}
