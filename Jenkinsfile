node {
    def app

//    stage('Clone repository') {
  //      /* Cloning the Repository to our Workspace OK*/

  //      checkout scm
  //  }
	
    stage('SCM Checkout'){
     git credentialsId: 'git-credential', url: https://github.com/chetanpatel1975/NodeApp'
   
      }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("chetankumarpatel/nodeapp")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
}
