pipeline {
   agent any
   tools {
      maven 'Maven'
   }
   stages {
       stage("build") {
           steps {
              snDevOpsStep()
               echo "Building" 
                sh 'mvn clean install -DskipTests'
               //sleep 5
           }
       }
       
     stage("test") {
           stages {
            stage('UAT unit test1') {
                steps {
                        //snDevOpsStep ()
                        echo "Testing"
                        sh 'mvn -Dtest=com.sndevops.eng.AppTest test'
                }                       
            }
            stage('UAT unit test 2') {
                 steps {
                         snDevOpsStep ()
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
                        //snDevOpsStep ()
                        echo "Testing"
                        echo "Testing"
                       // sh 'mvn -Dtest=com.sndevops.eng.AppTest test'
                }                    
        }

       stage("deploy") {
         stages{
             stage('deploy UAT') {
               steps{
                 snDevOpsStep ()
                 echo "deploy in UAT"
               }
             }
            stage('deploy PROD') {
                steps{
                  snDevOpsStep ()
                   echo "deploy in prod"
                  snDevOpsChange()              
                }
            }
        }
      }
     
    }
     
  }
