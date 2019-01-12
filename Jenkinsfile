pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'gradle build'
        sh 'gradle javadoc'
        sh 'gradle uploadArchives'
      }
    }
    stage('Code Analysis') {
      steps {
        sh 'sonar-scanner'
        waitForQualityGate true
      }
    }
  }
}