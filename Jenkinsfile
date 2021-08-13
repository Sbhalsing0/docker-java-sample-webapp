pipeline {
    agent {
        node {
            label 'jenkins-slave'
        }
    }
    stages { 	
        stage('Build Jar') {
            steps {
                echo "Hello Team"'
            }
        }
        stage('Build Image') {
            steps {
                script {
                	app = docker.build("sbhalsing0/jenkins")
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
			docker.withRegistry('https://registry.hub.docker.com', 'sanket') {
			app.push("${BUILD_NUMBER}")
			app.push("latest")
			        }
                }
            }
        }        
    }
}
