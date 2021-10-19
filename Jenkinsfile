pipeline{

	agent { dockerfile true }

	environment {
		DOCKERHUB_CREDENTIALS=credentials('alex4nder-dockerhub')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t alex4nder/myrepo:latest .'
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