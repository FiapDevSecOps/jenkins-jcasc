pipeline {
    agent any

    environment {
        GIT_SSH_COMMAND = 'ssh -o StrictHostKeyChecking=no' // Skip host key checking
        CONTAINER = 'jenkins-master'
        USER = 'rosthan'
        TAG = 'v1'
        DOCKERFILE_PATH = 'Dockerfile.master'

    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/FiapDevSecOps/jenkins-jcasc.git'
            }
        }

        stage('Jenkins Master - Build e Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'HUB_USER', passwordVariable: 'HUB_TOKEN')]) {                      
                    sh '''
                        docker login -u $HUB_USER -p $HUB_TOKEN 
                        docker build -t ${USER}/${CONTAINER}:${TAG} -t ${USER}/${CONTAINER}:latest. -f ${DOCKERFILE_PATH}
                        docker push ${USER}/${CONTAINER}:${TAG}
                    '''
                }
                
                // Add your build and test steps here
            }
        }

           stage('Jenkins Slaves - Build e Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'HUB_USER', passwordVariable: 'HUB_TOKEN')]) {                      
                    sh '''
                        docker login -u $HUB_USER -p $HUB_TOKEN 
                        docker build -t ${USER}/jenkins-ssh:${TAG} -t ${USER}/jenkins-ssh:latest. -f Dockerfile.ssh.agent
                        docker push ${USER}/${CONTAINER}:${TAG}
                    '''
                }
                
                // Add your build and test steps here
            }
        }
    }
}
