node ('ubuntu-app-agent'){  
    def app
    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */
       checkout scm
    }  
    
    stage('Build-and-tag') {
        /* This builds the actual image */
       sh 'echo ###Building docker image from source###'
        app= docker.build("amareshpattnaik6/snake")
    } 
    
    stage('Post-to-dockerhub') {
		/* This Pushes the image to image registry. */
       docker.withRegistry('https://registry.hub.docker.com', '	docker-auth') {
            app.push("latest")
       }
    }
	
	stage('Pull-image-server') {
		/* This stops the server, pull the latest image from image registry and start the service  */
         sh "docker-compose down"
         sh "docker-compose up -d"	
    }
}
