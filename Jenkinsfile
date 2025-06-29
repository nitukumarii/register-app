pipeline {
    agent { label 'Jenkin-Agent' }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    environment {
	    APP_NAME = "register-app-pipeline"
            RELEASE = "1.0.0"
            DOCKER_USER = "sonali1897"
            IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
            IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
	    
    }
    stages{
        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
        }

        stage("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/sonali18vats/register-app.git'
                }
        }

        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

       }

       stage("Test Application"){
           steps {
                 sh "mvn test"
           }
       }
        stage("SonarQube Analysis"){
           steps {
	           script {
		        withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') { 
                        sh "mvn sonar:sonar"
		        }
	           }	
           }
       }
	stage("Quality Gate") {
                  when {
                             expression { false }  // This condition disables the stage
                            }
                 steps {
                      script {
                        waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonarqube-token'
                   }
               }
	    }
         stage("Build & Push Docker Image") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'Dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    script {
                        def imageTag = "${RELEASE}-${env.BUILD_NUMBER}"
                        def imageName = "${DOCKER_USER}/${APP_NAME}"

                        docker.withRegistry("https://index.docker.io/v1/", 'Dockerhub') {
                            def dockerImage = docker.build(imageName)
                            dockerImage.push(imageTag)
                            dockerImage.push("latest")
			  }
		       }
                }
           }
       }
 }
}	
	    
	
