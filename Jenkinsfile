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
                    sh "docker build -t jkiran307/calculator ."
               }
          }
          
          stage("Docker login") {
               steps {
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'Docker-Cred',
                               usernameVariable: 'docid', passwordVariable: 'docpwd']]) {
                         sh "docker login --username $docid --password $docpwd"
                    }
               }
          }
          
          stage("Docker push") {
               steps {
                    sh "docker push jkiran307/calculator"
               }
          }
     }
}
