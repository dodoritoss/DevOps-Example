node {
    // reference to maven-3.8.7
    // ** NOTE: This 'maven-3.8.7' maven-3.8.7 tool must be configured in the Jenkins Global Configuration.   
    def mvnHome = tool 'maven-3.8.7'

    // holds reference to docker image
    def dockerImage
    // ip address of the docker private repository(nexus)
 
    def dockerImageTag = "devopsexample${env.BUILD_NUMBER}"
    
    stage('Clone Repo') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/felipemeriga/DevOps-Example.git'
      // Get the maven-3.8.7 tool.
      // ** NOTE: This 'maven-3.8.7' maven-3.8.7 tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'maven-3.8.7'
    }    
  
    stage('Build Project') {
      // build project via maven-3.8.7
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
	  
	  sh "docker run --name devops -d -p 2222:2222 devopsexample:${env.BUILD_NUMBER}"
	  
	  // docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
      //    dockerImage.push("${env.BUILD_NUMBER}")
      //      dockerImage.push("latest")
      //  }
      
    }
}
