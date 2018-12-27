pipeline {
    agent {
        node {
            label 'docker' && 'maven'
        }
    }
    stages { 	
        stage('Build Jar') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }
        stage('Build Image') {
            steps {
                script {
                	app = docker.build("astor4ever/docker")
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
			        docker.withRegistry('159.65.115.152', 'dockerhub') {
			        	app.push("${BUILD_NUMBER}")
			            app.push("latest")
			        }
                }
            }
        }        
    }
}