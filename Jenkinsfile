pipeline {
  agent any
  stages {
    stage('Parallel execution') {
      parallel {
        stage('Say hello') {
          steps {
            sh 'echo "hello world"'
          }
        }

        stage('build app') {
          agent {
            docker {
              image 'gradle:6-jdk11'
            }
          }
          steps {
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'

            // Cleanup steps
            echo 'Listing workspace contents before deletion...'
            sh 'ls -la'
            echo 'Deleting workspace...'
            deleteDir()
            echo 'Listing workspace contents after deletion...'
            sh 'ls -la'
          }
        }
      }
    }
  }
}