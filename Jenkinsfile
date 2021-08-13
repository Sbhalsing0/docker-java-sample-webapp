pipeline {
    agent none
    parameters {
      choice(name: 'Environment', choices: ['prod','qa'], description: 'Setting this will deploy the services on selected environment')
    }
    environment {
        //QA
        DOCKER_IMAGE_NAME_QA = "hello-jenkins"
        DOCKER_REGISTRY_PATH_QA = "sbhalsing0/jenkins"
        registryCredential = 'dockerhub_id'
        //prod
        DOCKER_IMAGE_NAME_PROD = "hello-jenkins-prod"
        DOCKER_REGISTRY_PATH_PROD = "sbhalsing0/popeye"
        registryCredential = 'dockerhub_id'
    }
    stages {
        stage('Example Build') {
            agent { docker 'jenkins_slave' } 
            steps {
                echo 'Hello, Maven'
            }
        }
    }
        stage('Build and Push Docker Image QA Env') {
        when {
          expression {
            return ((params.Environment == 'qa' && env.BRANCH_NAME == 'master')) 
          }
        }
    }
            steps {
                script {
                   app = docker.build(DOCKER_IMAGE_NAME_QA)
                   docker.withRegistry(DOCKER_REGISTRY_PATH_QA, ecrcred_qa) {
                   app.push("${env.GIT_COMMIT}")
                    }
                }
        }
}
