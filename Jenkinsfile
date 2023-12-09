pipeline{
    agent { label "dev-server" }
    stages{
        stage("Code"){
            steps{
                git url : "https://github.com/ReddyYashoda/node-todo-cicd.git", branch : "master"
            }
            
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t node-app-test"
            }
            
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"DockerHubPass",usernameVariable:"DockerHubUser")]){
                sh "docker image tag node-app-test ${env.DockerHubUser}/node-app-test:latest"
                sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                sh "docker push ${env.DockerHubUser}/node-app-test:latest"
                } 
            }
            
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }    
}
