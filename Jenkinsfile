pipeline {
  agent any
  environment{
        HELM_PATH=''
        BRANCH='master'
        MAJ_VER='1.0'
        DOCKER_CREDS=credentials('docker-creds')
    }
  stages {
    stage ('build docker images'){
      steps{
        echo "building docker images"
        script{
          dir('node-app/'){
          sh 'docker build . -t hp-home'
        }
        }
      }
    }
    stage('docker push images'){
      steps{
        echo "Pushing docker images"
        script{
          sh 'docker tag hp-home:latest $DOCKER_CREDS_USR/hp-home:$MAJ_VER.${env.BUILD_ID}'
          sh 'echo $DOCKER_CREDS_PSW | docker login -u $DOCKER_CREDS_USR --password-stdin'
          sh 'docker push $DOCKER_CREDS_USR/HP-HOME:$MAJ_VER.${env.BUILD_ID}'
        }
        
      }
    }
  }
}
