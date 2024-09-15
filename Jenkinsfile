pipeline {
    agents any
    
    
    stages{
        stage("code"){
            steps {
                echo "cloning the code"
                git url:"https://github.com/Awaismalikhas/webapp.git", branch: "master"
            }
        }
      
        stage("build"){
            steps{   
                echo "building the code"
                sh "docker build -t my-web-app ."
            }
        }
        stage("push to docker hub"){
            steps{
                echo "pushing image to dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerHUb",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-web-app ${env.dockerHubUser}/my-web-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-web-app:latest"    
                }
            }
        }
        
        stage("deploy"){
                echo "deploying the code"
                sh "docker run -d -p 8000:8000"
            
        }
        
        
        
        
    }
    
    
}
