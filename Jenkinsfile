pipeline{

	agent any

	tools {nodejs "node"}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('alex4nder-dockerhub')
	}

	stages {

		stage('Install dependencies') {
			steps {
				sh 'npm install --prefix ./client'
			}
		}

		stage('Test') {
			steps {
				sh 'npm test --prefix ./client'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t alex4nder/myrepo:latest -f client/Dockerfile .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push alex4nder/myrepo:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}