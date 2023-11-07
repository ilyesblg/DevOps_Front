pipeline {

  agent any
  tools { nodejs "NodeJs" }

  stages {
    
    stage('Build Frontend') {
      steps {
        sh 'npm install' 
        sh 'npm run build'
      }
    }
    
    
    stage("Docker build Frontend"){
       steps {
        sh 'docker build -t devops_front_end .'
        sh 'docker image list'
        sh 'docker tag devops_front_end ilyesblg/devops_front_end:latest'
        
        withCredentials([string(credentialsId: 'DockerhubCred', variable: 'PASSWORD')]) {
            sh 'docker login -u ilsiyerisne74 -p $PASSWORD'
        }
       }
  }
  
  
  
    stage("Push Frontend Image to Docker Hub"){
      steps {
       sh 'docker push  ilyesblg/devops_front_end:latest'
    }
    }
    
    
    
  
  }
  post{
        always{
            sh 'docker logout'
        }
        success {            
            mail to :'boualleguiilyes1@gmail.com',
            subject : 'Successful Jenkins Build Of The Frontend',
            body : 'Great news! The Jenkins build of the angular frontend is a success.',
            from : 'ilyes.boualagui@gmail.com'
        }
        failure {
            mail to :'boualleguiilyes1@gmail.com',
            subject : 'Jenkins Build Of The Frontend Failed',
            body : 'Unfortunately, the Jenkins build of the angular frontend has encountered an issue and failed.',
            from : 'ilyes.boualagui@gmail.com'
        }
    }
}
