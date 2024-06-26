pipeline {
  agent any
  
   tools {nodejs "node"}
    
  stages {
    stage("cloning git in GitHub") {
            steps {
                script {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GITHUB_CREDENTIALS', url: 'https://github.com/david19121/deploy-nodeapp-jenkins22.git']])
                    //git branch: 'main', url: 'https://github.com/david19121/deploy-nodeapp-jenkins22.git' 
                }
            }
        }
     
    stage('intialising npm installation.......') {
      steps {
        sh 'npm install'
      }
    }
  
     stage('Building Docker Image') {
            steps {
                script {
                 
                  sh 'printenv'
                  sh 'git version'
                  //sh 'docker build -t david19121/node-app:""$Build_ID"".'
                  sh 'docker build -t david19121/node-app1 .'
                }
            }
        }


        stage('Deploying the Docker Image to DockerHub') {
            steps {
                script {
                 withCredentials([string(credentialsId: 'dockerhub_ID', variable: 'dockerhub_ID')]) {
                    sh 'docker login -u david19121 -p ${dockerhub_ID}'
            }

            //sh 'docker push david19121/node-app:""$Build_ID""'
            sh 'docker push david19121/node-app1:latest'
        }
            }   
        }
         
     

  }
}

	
