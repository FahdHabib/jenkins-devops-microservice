//SCRIPTED PIPELINE - OLD WAY
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Deploy') {
// 		echo "Deploy"
// 	}
// }

//DECLARATIVE 
pipeline {
	//agent any
	agent { docker { image 'python:alpine3.18'}}
	stages {
		stage('Build') {
			steps {
				sh 'python --version'
				echo "Build"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Deploy') {
			steps {
				echo "Deploy"
			}
		}
	} 
	post {
		always {
			echo "I run always."
		}
		success {
			echo "I run when build is successful."
		}
		failure {
			echo "I run when build fails."
		}
	}
}