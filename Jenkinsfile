node{
    
   def buildNumber = BUILD_NUMBER
   def mavenHome = tool name: "maven3.8.6"
   
    stage("Git CheckOut"){
         git credentialsId: '7af5a31e-4991-41fe-888d-65b11501ebc5', url: 'https://github.com/sunny00000000/java-web-app-docker.git'
    }
    
    stage(" Maven Clean Package"){
      sh "${mavenHome}/bin/mvn clean package"
    } 
    
    stage("Build Dokcer Image") {
         sh "docker build -t sunny00000000/java-web-app:${buildNumber} ."
    }
    
    
    stage("Docker Push"){
        sh "docker login -u sunny00000000 -p Sunny007@"
        sh "docker push sunny00000000/java-web-app:${buildNumber}"
    }

   stage("Deploy to docker swarm cluster"){
       sshagent(['d36fdb1d-9d9b-451a-91e8-440f286425fe']) {
      sh "ssh ubuntu@18.207.126.96 docker service create --name javawebapp -p 7070:8080 --replicas 2  sunny00000000/java-web-app:${buildNumber}"
    }
  }
}

