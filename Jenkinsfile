pipeline {
  agent {
    node {
      label 'master'
    }

  }
  tools {
    gradle "gradle6"
  }
  stages {
    stage('Source') {
      steps {
        git 'https://github.com/dhlee56/jenkins-blueocean-gradle.git'
      }
    }

    stage('Build') {
      steps {
        sh 'gradle bootJar'
      }
    }

  }
}
