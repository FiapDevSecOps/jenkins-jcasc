pipeline {
    agent any

    environment {
        GIT_SSH_COMMAND = 'ssh -o StrictHostKeyChecking=no' // Skip host key checking
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'your_branch', credentialsId: 'github', url: 'git@github.com:FiapDevSecOps/jenkins-jcasc.git'
            }
        }

        stage('Build Master') {
            steps {
                // Add your build and test steps here
            }
        }

        stage('Push Master') {
            steps {
                // Add deployment steps here
            }
        }
    }
}

// pipeline {
//   environment {
//     registry = 'rosthan/jenkins-master'
//     registryCredential = 'jenkins-ssh-github'
//     dockerImage = ''
//   }

//   agent any
//   stages {
//     stage('Cloning our Git') {
//       steps {
//         git branch: 'main', credentialsId: 'jenkins-ssh-github', url: 'git@github.com:rosthan/jenkins-jcasc.git'
//       }
//     }

//     stage('Building Docker Image') {
//       steps {
//         script {
//           withCredentials([string(credentialsId: 'PORT', variable: 'PORT')]) {
//             dockerImage = docker.build("$registry:$BUILD_NUMBER", "--build-arg PORT=$PORT .")
//           }
//         }
//       }
//     }

//     stage('Deploying Docker Image to Dockerhub') {
//       steps {
//         script {
//           docker.withRegistry('', registryCredential) {
//             dockerImage.push()
//           }
//         }
//       }
//     }

//     stage('Cleaning Up') {
//       steps {
//         sh "docker rmi --force $registry:$BUILD_NUMBER"
//       }
//     }
//   }
// }