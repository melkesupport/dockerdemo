pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('amonkincloud-dockerhub')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh 'docker build -t demoinsuranceapi/flaskapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
	     sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW docker.io'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push demoinsuranceapi/flaskapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
