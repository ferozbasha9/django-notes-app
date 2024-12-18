pipeline {

agent { label "dev"}

stages{
 stage("Code clone"){
  steps{
   git url : "https://github.com/ferozbasha9/django-notes-app.git", branch : "main"
       }
      }
 stage("Build"){
  steps{
   sh "docker build . -t notesappimage-jenkins"
       }
 }
 stage("Push to dockerhub"){
  steps{
   withCredentials(
   [usernamePassword(
   credentialsId:"dockerCreds",
   passwordVariable:"dockerHubPass",
   usernameVariable:"dockerHubUser"
)
]
){
sh "docker image tag notesappimage-jenkins ${env.dockerHubUser}/notesappimage-jenkins"
sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
sh "docker push ${env.dockerHubUser}/notesappimage-jenkins"
}
}
}
 stage("Deploy"){
  steps{
   sh "docker compose up -d"
       }
      }
 }
}



