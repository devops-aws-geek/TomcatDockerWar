pipeline {
     agent any
     stages {
          stage("Compile") {
               steps {
                    sh "/var/lib/jenkins/sw/maven/bin/mvn compile"
               }
          }
          stage("Unit test") {
               steps {
                    sh "/var/lib/jenkins/sw/maven/bin/mvn test"
               }
          }
     
    
stage("Package") {
     steps {
          sh "/var/lib/jenkins/sw/maven/bin/mvn package"
     }
}
stage("Docker build") {
     steps {
      
          sh "docker build -t deepak_tomcat ."
     }
}

stage("Deploy to staging") {
     steps {
          
          sh "docker stop \$(docker ps -qa)"
          sh "docker rm \$(docker ps -qa)"
          sh "docker run -d -it -v /var/lib/jenkins/workspace/tomcat-dockerize-app-demo/target/:/usr/local/tomcat/webapps/ -p 8081:8080 --name Testtomcat deepak_tomcat"
     }
}

     }
  post {
     always {
          sh "echo 'I did It'"
     }
}
}
