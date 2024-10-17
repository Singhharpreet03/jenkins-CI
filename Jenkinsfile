pipeline {
  agent any
  environment{
        HELM_PATH='Singhharpreet03/testapp-helm-repo'
        BRANCH='main'
        MAJ_VER='1.0'
        DOCKER_CREDS=credentials('docker-creds')
        GITHUB_TOKEN=credentials('github-token')
    }
  stages {
    stage ('build docker images'){
      steps{
        echo "building docker images "
        script{
          dir('node-app/'){
          sh 'docker build . -t hp-home'
        }
        }
      }
    }
    stage('docker push images') {
    steps {
        echo "Pushing docker images"
        script {
            sh '''
                docker tag hp-home:latest $DOCKER_CREDS_USR/hp-home:$MAJ_VER.$BUILD_ID
                echo $DOCKER_CREDS_PSW | docker login -u $DOCKER_CREDS_USR --password-stdin
                docker push $DOCKER_CREDS_USR/hp-home:$MAJ_VER.$BUILD_ID
            '''
          }
       }
     }
    stage('update helm repo'){
      steps{
      sh '''
         git clone https://x-access-token:$GITHUB_TOKEN@github.com/$HELM_PATH
         cd testapp-helm-repo
         git checkout $BRANCH
         '''
      dir('testapp-helm-repo'){
        sh ''' 
          sed -i "s|tag: .*|tag: $MAJ_VER.$BUILD_ID|g" values.yaml
          '''
        sh '''
          git config user.name "Singhharpreet03"
          git config user.email "harpreet152436@gmail.com"
          git add -A
          git commit -m "updated image to tag number $MAJ_VER.$BUILD_ID"
          git push https://x-access-token:$GITHUB_TOKEN@github.com/Singhharpreet03/testapp-helm-repo.git $BRANCH
          '''
      }
      }
    }
  }
      }
    
 
