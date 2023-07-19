pipeline {
   agent any
   tools {
      maven 'Maven'
   }
   stages {
        stage('Prep') {
            steps {
//                deleteDir()
            }
        }
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
           stage('Custom Test Step') {
                   steps {
                     sh '''
                       echo "{\\"name\\":\\"Functional Test Suite\\",\\"result\\":\\"fail\\",\\"buildNumber\\":\\"$BUILD_NUMBER\\",\\"stageName\\":\\"Test\\",\\"pipelineName\\":\\"$JOB_NAME\\"}" > functional-results.json
                     '''
                     archiveArtifacts artifacts: '**/functional-results.json'
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

       stage("deploy") {
         stages{
            stage('register') {
               steps {
                  snDevOpsArtifact(artifactsPayload: """{"artifacts": [{"name": "mbartifact", "version": "1.0.${env.BUILD_NUMBER}","semanticVersion": "1.0.${env.BUILD_NUMBER}","repositoryName": "mbrepository"}]}""")
               }
            }
            
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
    post {
       always {
          deleteDir()
       }
    }
  }
