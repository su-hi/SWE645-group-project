pipeline{
	agent any 
	environment{
		registry = "khadijakobra/hw2"
		DOCKERHUB_PASS = "docker645"
		 unique_Id = UUID.randomUUID().toString()
		
	}
	stages{
		stage("Building jar"){
			steps{
				script{
					checkout scm
					sh 'rm -rf *.war'
					sh 'jar -cvf HW2.war -C WebContent/ .'
					sh 'echo ${BUILD_TIMESTAMP}'
					sh 'docker login  -u khadijakobra -p ${DOCKERHUB_PASS}'
					def customimage=docker.build("khadijakobra/hw2:${BUILD_ID}.${unique_Id}")
					

					
			}

		}

	}
	stage("Pushing image to DockerHub"){
		steps{
			script{
				sh 'docker push khadijakobra/hw2:${BUILD_ID}.${unique_Id}'
			}
		}
	}
		
	stage("Rancher single pod deploy"){
	         steps{
	         	sh 'kubectl set image deployment/hw2 hw2=khadijakobra/hw2:${BUILD_ID}.${unique_Id} -n jenkins-pipeline'
	         }
	    }
	
	stage("With Load Balancer"){
	   	steps{
	    	sh 'kubectl set image deployment/hw2-lb hw2-lb=khadijakobra/hw2:${BUILD_TIMESTAMP} -n hw2'
	    }
	}

}




}
