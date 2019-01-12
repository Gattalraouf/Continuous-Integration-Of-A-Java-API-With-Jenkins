pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'gradle build'
        sh 'gradle javadoc'
        sh 'gradle jar'
        sh 'archiveArtifacts \'build/libs/*.jar\''
      }
    }
    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            sh '/home/asta/Servers/sonar-scanner-cli-3.3.0.1492-linux/sonar-scanner-3.3.0.1492-linux/bin/sonar-scanner '
          }
        }
        stage('Test reporting') {
          steps {
            jacoco(deltaInstructionCoverage: '60')
          }
        }
      }
    }
    stage('Deployment') {
      steps {
        sh 'gradle uploadArchives'
      }
    }
    stage('Slack Notification') {
      steps {
        slackSend(message: 'Testing Jenkins')
      }
    }
  }
}