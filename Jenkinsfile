pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'gradle build'
        sh 'gradle javadoc'
        sh 'gradle jar'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/'
      }
      post {
        failure {
          mail(subject: 'Jinkens Test Failed', body: 'Mail Notification of the  Integration JAVA API with Jenkins', bcc: 'fa_gattal@esi.dz ', cc: 'fm_boutemine@esi.dz')
        }
      }
    }

    stage('Mail Notification') {
      steps {
         mail(subject: 'Jinkens Test Successful', body: 'Mail Notification of the  Integration JAVA API with Jenkins', bcc: 'fa_gattal@esi.dz ', cc: 'fm_boutemine@esi.dz')
      }
    }
    
    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonarqube') {
              sh '/home/asta/Servers/sonar-scanner-cli-3.3.0.1492-linux/sonar-scanner-3.3.0.1492-linux/bin/sonar-scanner '
            }

            waitForQualityGate true
          }
        }
        stage('Test reporting') {
          steps {
            jacoco(minimumInstructionCoverage: '60', minimumLineCoverage: '60', minimumMethodCoverage: '60', minimumComplexityCoverage: '60', minimumClassCoverage: '60', minimumBranchCoverage: '60', maximumMethodCoverage: '90', maximumLineCoverage: '90', maximumInstructionCoverage: '90', maximumComplexityCoverage: '90', maximumClassCoverage: '90', maximumBranchCoverage: '90')
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

