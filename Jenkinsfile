pipeline {
   agent any
   tools {
      maven 'Maven'
   }
   stages {
       stage("build") {
           steps {
               echo "Building" 
                sh 'mvn clean install -DskipTests'
               //sleep 5
           }
       }
       
     stage("test") {
           stages {
            stage('UAT unit test1') {
                steps {
                        echo "Testing"
                        sh 'mvn -Dtest=com.sndevops.eng.AppTest test'
                }                       
            }
            stage('UAT unit test 2') {
                 steps {
                        echo "Testing"
                        sh 'mvn -Dtest=com.sndevops.eng.App1Test test'                     
                }
            }     
        }
          post {
              always {
              junit '**/target/surefire-reports/*.xml' 
              }
        }
      
      }
           
      stage("test-1") {
                steps {
                        echo "Testing"
                        echo "Testing"
                        sh 'mvn -Dtest=com.sndevops.eng.AppTest test'
                }                    
        }

      stage("register") {
                steps {
                snDevOpsArtifact(artifactsPayload: """{"artifacts": [{"name": "mbartifact", "version": "1.0.${env.BUILD_NUMBER}","semanticVersion": "1.0.${env.BUILD_NUMBER}","repositoryName": "mbrepository"}]}""")
                snDevOpsPackage(name: "mbpackage", artifactsPayload: """{"artifacts":[{"name": "mbartifact", "version": "1.0.${env.BUILD_NUMBER}", "repositoryName": "mbrepository"}""")
        }
      }

       stage("deploy") {
         stages{
             stage('deploy UAT') {
               steps{

                 echo "deploy in UAT"
               }
             }
            stage('deploy PROD') {
                steps{
                   echo "deploy in prod"
                  snDevOpsChange()              
                }
            }
        }
      }
     
    }
     
  }
