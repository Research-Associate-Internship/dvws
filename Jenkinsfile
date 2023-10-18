pipeline {
	agent {
		label 'vi-ubuntu'
	}
	stages {
		stage ("Git checkout"){
			steps {
				git branch: "master",
					url: "https://github.com/Research-Associate-Internship/dvws"
				sh "ls"
			}
		}
		stage ("Git Secrets"){
			steps{
				sh "rm trufflehog || true"
				sh "docker run gesellix/trufflehog --json https://github.com/Research-Associate-Internship/dvws > trufflehog"
				sh "cat trufflehog"
			}
		}
		stage ("Python Bandit Security Scan"){
			steps{
				sh "docker run --rm --volume \$(pwd) secfigo/bandit:latest"
			}
		}
		
		stage ("Static Analysis with python-taint"){
			steps{
				sh "docker run --rm --volume \$(pwd) vickyrajagopal/python-taint-docker pyt ."
			}
		}					
	}
}
