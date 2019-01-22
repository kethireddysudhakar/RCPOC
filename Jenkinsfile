node {
   stage('SCM CheckOut'){
      
       git credentialsId: '0af3239f-f8a4-4d22-9ea7-b583b599e472', url: 'https://github.com/kethireddysudhakar/RCPOC'
   
       
   }

    stage('MVN Package'){
        def mvnHome= tool name: 'POCMaven', type: 'maven'
        def mvncmd="${mvnHome}/bin/mvn"
        bat label: '', script: "${mvncmd} clean package"
    }
    
    stage('Docker Build Image'){
        
       bat 'docker build -t sudhakarkethireddy/testpoc:2.0 .'
    }
    
     stage('Docker Push Image'){
         
         withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerPwd')]) {
            // some block
            
              bat "docker login -u sudhakarkethireddy -p  ${dockerPwd}"
         }
        
      
       bat 'docker push sudhakarkethireddy/testpoc:2.0'
    }
    
    stage('Run Docker Container'){
        bat 'docker run -p 8081:8080 -d --name testpoc sudhakarkethireddy/testpoc:2.0'
    }
    
}

