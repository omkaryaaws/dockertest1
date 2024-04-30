pipeline {


	agent any
	stages {
		stage('Clone Repo') {
			steps {
				sh 'rm -rf dockertest1'
                sh 'git clone https://github.com/omkaryaaws/dockertest1.git'
            }
		}
	}
		
		stage('Build Docker Image') {
			steps {
				
				sh 'cd var/lib/jenkins/workspace/pipeline1/dockertest1_master'
				sh 'docker rmi omkaryacool/docker-test:pipe1'
				sh 'docker build -t omkaryacool/docker-test:pipe1 .'
		}
	}
	
		stage('push image to docker hub') {	
			steps {
				sh  'docker push omkaryaaws/docker-test:pipe1'
			}
		}
			
		stage ('Deploy') {
			steps {
				sh 'docker -H tcp://172.31.0.111:2375 stop webapp1'
				sh 'docker -H tcp://172.31.0.111:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 omkaryaaws/docker-test:pipe1'
			}
		}
		   
		stage('check Reach') {
			steps {
				sh 'sleep 30s'
				sh 'curl http://ec2-43-204-110-113.ap-south-1.compute.amazonaws.com:9000'
			}
			
	   }
 }
