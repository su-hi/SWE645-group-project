/* Submitted by #Taseef Rahman & Mahbubul Alam Palash
Jenkins file for building application using Docker & Deploying them in Google Kubernete Engine Cluster
*/
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
					sh 'jar -cvf HW2.war -C /WebContent/ .'
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
		
	stage(' Deploying updated image to GKE'){
		steps{
			sh ' kubectl set image  deployment/swe645hw2 student=swe645/hw2:${BUILD_ID}.${unique_Id}'
			
		}

	}

}




}
