node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build Image') {
        /* This builds the actual image */

        app = docker.build("sherwinamihan/data-rest")
    }

    stage('Test Image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push Image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('', 'dockerHub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
}
