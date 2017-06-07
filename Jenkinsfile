pipeline {
    agent none
    stages {
        stage('Build') {
            agent any
            steps {
								sh 'cd cachecloud-open-web'
                sh 'mvn clean compile install -Plocal'
            }
        }
	}
}
