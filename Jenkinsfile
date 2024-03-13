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
  }
}
