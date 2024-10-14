pipeline {
  agent any
  stages {
    stage ('build basic app'){
      steps{
        sh ' docker compose up -f /test/. --build'
        sh ' echo "voting app is deployed" '
      }
    }
    stage ('build node app') {
      steps{
        sh ' docker compose up -f /node-app/. --build '
        sh ' echo " node based home page deployed" ' 
      }
    }
  }
}
