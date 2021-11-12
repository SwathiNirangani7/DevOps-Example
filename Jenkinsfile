node {   
    def mvnHome = tool 'M3'
    def dockerImage
    def dockerImageTag = "devopsexample${env.BUILD_NUMBER}"
    
    stage('Clone Repo') { 
      git 'https://github.com/SwathiNirangani7/DevOps-Example.git'          
      mvnHome = tool 'M3'
    }    
  
    stage('Build Project') {
      // build project via maven
      sh "'${mvnHome}/bin/mvn' clean install"
    }
		
    stage('Build Docker Image') {
      // build docker image
      dockerImage = docker.build("devopsexample:${env.BUILD_NUMBER}")
    }
   
    stage('Deploy Docker Image'){
      
      // deploy docker image to nexus
		
      echo "Docker Image Tag Name: ${dockerImageTag}"
	  
	  sh "docker stop devopsexample"
	  
	  sh "docker rm devopsexample"
	  
	  sh "docker run --name devopsexample -d -p 2222:2222 devopsexample:${env.BUILD_NUMBER}"
	  
	  // docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
      //    dockerImage.push("${env.BUILD_NUMBER}")
      //      dockerImage.push("latest")
      //  }
      
    }
}
