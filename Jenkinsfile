pipeline{
	agent {  docker { image 'python:3.7-slim'} }
	stages {
		stage('Build'){
			steps {
				sh 'python3 --version'
				echo "Build"
			}
		}
		stage('Test'){
			steps {
				echo "Test"
			}
		}
		stage("Build Docker"){
			steps{
				script{
					dockerImage = docker.build("dhruvpanchal96/flasktest:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push to hub'){
			steps{
				script {
					docker.withRegistry('', 'dockerhub')
					dockerImage.push();
					dockerImage.push('latest')
				}
			}
		}
		
	}
	post {
		always {
			echo "I always run"
		}
		success {
			echo "I run on success"
		}
		failure {
			echo "I run on failure"
		}
	}
}
