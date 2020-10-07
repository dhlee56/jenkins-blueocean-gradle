pipeline {
  agent {
    node {
      label 'master'
    }

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

    stage('Run') {
      steps {
        sh 'java -jar build/libs/sia5.ch02-0.0.1-SNAPSHOT.jar'
      }
    }

  }
  tools {
    gradle 'gradle6'
  }
}