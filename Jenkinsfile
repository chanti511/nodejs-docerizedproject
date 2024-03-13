pipeline{
  agent any
      environment {
        DOCKER_REGISTRY = 'chanti511'
        DOCKER_REPO = 'nodejs'
        IMAGE_NAME = 'mynodeapp'
        TAG = 'latest'
    }
  stages{
    stage("Checkout")
    {
      steps{
        checkout scm
      }
    }
    stage("Npm Installation")
    {
      steps{
        bat 'npm install npm@latest -g'
        bat 'npm test'
      }
    }
    stage("Build")
    {
      steps{
        bat 'npm run build'
      }
    }
    stage("Build Image")
    {
      steps{
        bat "docker build -t ${DOCKER_REGISTRY}/${DOCKER_REPO}/${IMAGE_NAME}:${TAG} ."
      }
    }
    stage('Push Docker Image') {
            steps {
                // Login to Docker registry using credentials stored in Jenkins
                withCredentials([usernamePassword(credentialsId: 'docker-credentials-id', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    bat "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD} ${DOCKER_REGISTRY}"
                }

                // Push Docker image to repository
                bat "docker push ${DOCKER_REGISTRY}/${DOCKER_REPO}/${IMAGE_NAME}:${TAG}"
            }
  }
}
}
