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
                   script {
                     snDevOpsArtifact(artifactsPayload: """{"artifacts": [{"name": "mbartifact", "version": "1.${env.BUILD_NUMBER}.0","semanticVersion": "1.${env.BUILD_NUMBER}.0","repositoryName": "mbrepo"}])
                     //snDevOpsPackage(name: "${packageName}", artifactsPayload: """{"artifacts": [{"name": "${applicationJar}", "version": "2.${env.BUILD_NUMBER}.0","semanticVersion": "1.0.0","repositoryName": "test3"}], "branchName": "master"}""")
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
