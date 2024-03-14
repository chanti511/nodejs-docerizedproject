pipeline{
  agent any
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
        bat "docker build -t my-node-app:1.1 ."
      }
    }
    stage('Push Docker Image') {
            steps {
                // Login to Docker registry using credentials stored in Jenkins
              withCredentials([usernamePassword(credentialsId: 'github_cred', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')])
              {
                    bat "docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                    bat "docker tag my-node-app:1.1 chanti511/my-node-app:1.1"
                    bat "docker push chanti511/my-node-app:1.1"
                }
            }
  }
}
}
