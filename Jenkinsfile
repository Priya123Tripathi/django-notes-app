@Library('shared') _
pipeline{
   agent {label 'vinod'}

   stages{
       stage("hello"){
          steps{
             script{
                 hello()
             }
          }
       }
       stage("Code"){
           steps{
                script{
                    clone("https://github.com/Priya123Tripathi/django-notes-app.git" ,"main")
                }
           }
       }
       stage("Build"){
           steps{
               script{
                   docker_build("django_app","latest","priatripathi")
               }
           }
       }
       stage("Test"){
           steps{
               echo "This is testing the code"
           }
       }
        stage("Push to DockerHub"){
           steps{
             docker_push(
               imageName: "priatripathi/django_app",
               imageTag: "latest",
               credentials: "dockerhubcred"
        )
    }
}
       stage("Deploy"){
           steps{
               sh "docker compose down || true"
               sh "docker compose down && docker compose up -d"
           }
       }
   }
}
