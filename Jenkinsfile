pipeline {
  agent any
  stages {
    stage ('build basic app'){
      steps{
        sh 'docker-compose -f /test/docker-compose.yaml up --build'
        sh ' echo "voting app is deployed" '
      }
    }
    stage ('build node app') {
      steps{
        sh ' docker compose up -f /node-app/docker-compose.yaml --build '
        sh ' echo " node based home page deployed" ' 
      }
    }
  }
}
