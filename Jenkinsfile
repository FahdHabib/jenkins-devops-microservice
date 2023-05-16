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
	stages {
		stage('Build') {
			steps {
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
		fail {
			echo "I run when build fails."
		}
	}
}