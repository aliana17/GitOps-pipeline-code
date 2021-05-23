pipeline {
    environment {
    
    image_name = "anchal72/test"
    docker_image = ''
    
    }
    agent any

    stages {
        stage('Build') {
            
            steps {
		echo "Building..."
		    script {
			docker_image = docker.build image_name + ":$BUILD_NUMBER" 
		    }
	    }
        }
        stage('Test') {
	     agent {
		     docker {
		     	image 'python:3.5.1'
			args '-u root'
		     }
	     }
            steps {
                echo 'Testing..'
		sh 'python main.py'
            }
        }
        stage('Deploy') {
            steps {
                script {
			docker.withRegistry('','docker_hub') { 
		   		docker_image.push("$BUILD_NUMBER")
         
			}
		}
            }
        }
    }
}
