pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'gradle build'
        sh 'gradle test'
        sh 'gradle uploadArchives'
      }
    }
  }
}