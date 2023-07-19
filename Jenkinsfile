pipeline {
   agent any
   tools {
      maven 'Maven'
   }
   stages {
        stage('Prep') {
            steps {
                sh '''
                  ls -l
                '''
               deleteDir()
            }
        }
       
     stage("test") {
           stages {
              stage('Custom Test Step') {
                   steps {
                     sh '''
                       echo "{\\"name\\":\\"Functional Test Suite\\",\\"result\\":\\"fail\\",\\"buildNumber\\":\\"$BUILD_NUMBER\\",\\"stageName\\":\\"Test\\",\\"pipelineName\\":\\"$JOB_NAME\\"}" > functional-results.json
                     '''
                     archiveArtifacts artifacts: '**/functional-results.json'
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
