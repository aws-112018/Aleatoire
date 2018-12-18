pipeline {
  agent {
    docker {
      image 'cfinfrastructure/mkdocs'
      args '-p 3000:30000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'mkdocs build'
      }
    }
    stage('Test') {
      steps {
        sh 'ls -l site/'
      }
    }
    stage('Package') {
      steps {
        sh 'zip -r site.zip site/*'
        archiveArtifacts(artifacts: 'site.zip', caseSensitive: true)
      }
    }
    stage('Deliver') {
      steps {
        sh 'echo "Working on Delivery"'
        sh 'scp site.zip root@get.goffinet.org:/var/www/html/mkdocs-test/'
      }
    }
  }
}
