pipeline {
     agent any
     stages {
          
          stage("Compile") {
               steps {
                    sh "chmod +x gradlew"
                    sh "./gradlew compileJava"
               }
          }
          stage("Unit test") {
               steps {
                    sh "./gradlew test"
               }
          }
          stage("Package") {
               steps {
                    sh "./gradlew build"
               }
          }

          stage("Docker build") {
               steps {
                    sh "docker build -t anandbprem/calculator ."
               }
          }
          
          stage("Docker login") {
               steps {
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker-hub-credentials',
                               usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                         sh "docker login --username $USERNAME --password $PASSWORD"
                    }
               }
          }
          
          stage("Docker push") {
               steps {
                    sh "docker push anandbprem/calculator"
               }
          }
     }
}
