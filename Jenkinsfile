pipeline {
    environment {
    
    image_name = "anchal72/test"
    docker_image = ''
	    
    job_name = currentBuild.fullDisplayName
    
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
		emailext (
			subject: "STARTED: Job "${job_name} $BUILD_NUMBER",
		        body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
			<p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
		        recipientProviders: [[$class: 'DevelopersRecipientProvider']]
    		)

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
