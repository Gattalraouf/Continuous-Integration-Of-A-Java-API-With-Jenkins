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
    stage('Mail Notification') {
      steps {
        mail(subject: 'Jinkens Test', body: 'Mail Notification of the  Integration JAVA API with Jenkins', bcc: 'fa_gattal@esi.dz ', cc: 'fa_boutemine@esi.dz')
      }
    }
  }
}