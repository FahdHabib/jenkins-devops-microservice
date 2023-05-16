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
	agent any
	//agent { docker { image 'python:alpine3.18'}}
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				sh 'docker --version'
				sh 'mvn --version'
				echo "Build"
				echo "$PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID = $env.BUILD_ID"
				echo "JOB_NAME = $env.JOB_NAME"
				echo "BUILD_TAG = $env.BUILD_TAG"
				echo "BUILD_URL = $env.BUILD_URL"
			}
		}
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}

		stage('Build Docker Image'){
			steps {
				//"docker build -t in28min/currecy-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("in28min/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}

		stage('Push Docker Image'){
			steps {
				script {
					docker.withRegistry('','dockerhub') {
					dockerImage.tag('fahadhabib911/currency-exchange-devops');
					dockerImage.push('latest');
					}
				}
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