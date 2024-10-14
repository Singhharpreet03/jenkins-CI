pipeline {
  agent any
  stages {
    stage ('build basic app'){
      steps{
        sh ' pwd'
        sh ' ls -l'
        sh 'docker compose -f test/docker-compose.yaml up --build -d'
        sh ' echo "voting app is deployed" '
      }
    }
    stage ('build node app') {
      steps{
        sh ' docker compose up -f node-app/docker-compose.yaml --build -d '
        sh ' echo " node based home page deployed" ' 
      }
    }
  }
}
