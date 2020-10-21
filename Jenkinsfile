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
					def customimage=docker.build("khadijakobra/hw2:${BUILD_TIMESTAMP}")
					

					
			}

		}

	}
	stage("Pushing image to DockerHub"){
		steps{
			script{
				sh 'docker push khadijakobra/hw2:${BUILD_TIMESTAMP}'
			}
		}
	}
		
	stage("Rancher single pod deploy"){
	         steps{
	         	sh 'kubectl set image deployment/=khadijakobra/hw2:${BUILD_TIMESTAMP} --kubeconfig /var/lib/jenkins/.kube/config -n hw2'
	         }hw2image hw2image
	    }
	

}




}
