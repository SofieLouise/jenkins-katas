pipeline {
  agent any
  stages {
    stage('Parallel execution') {
      parallel {
        stage('Say Hello') {
          steps {
            sh 'echo "hello world"'
          }
        }

        stage('build app') {
          agent {
            docker {
              image 'gradle:jdk11'
            }

          }
          steps {
            sh 'sh ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
          }
        }

      }
    }

    stage('Clone Down') {
      agent {
        node {
          label 'host'
        }

      }
      steps {
        stash(name: 'code', excludes: '.git')
      }
    }

  }
}