pipeline{
	agent any
	environment{
		DOCKERHUB_PASS = 'docker645'
	}
	stages{
		stage("Student Survey"){
			steps{
				script{
					checkout scm
					sh 'rm -rf *.war'
					sh 'jar -cvf HW2.war -C WebContent/ .'
					sh 'echo ${BUILD_TIMESTAMP}'
					sh "docker login -u khadijakobra -p ${DOCKERHUB_PASS}"
					
				}
			}
		}
	    stage("Image pushing to DockerHub"){
	    	steps{
	    		script{
	    			sh 'docker push khadijakobra/hw2:${BUILD_TIMESTAMP}'
	    		}
	    	}
	    }
	    stage("Rancher single pod deploy"){
	         steps{
	         	sh 'kubectl set image deployment/hw2jenkins-pipeline hw2jenkins-pipeline=khadijakobra/hw2:${BUILD_TIMESTAMP} -n jenkins-pipeline'
	         }
	    }
	    stage("With Load Balancer"){
	    	steps{
	    			sh 'kubectl set image deployment/hw2-lb hw2-lb=khadijakobra/hw2:${BUILD_TIMESTAMP} -n jenkins-pipeline'
	    	}
	    }
	}
}	

