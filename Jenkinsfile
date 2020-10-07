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

    stage('Build docker file') {
      steps {
        sh 'docker build --build-arg JAR_FILE=build/libs/*.jar -t dhlee56/ch02tacos .'
      }
    }

    stage('Docker push') {
      steps {
        sh 'echo "docker run or push"'
      }
    }

  }
  tools {
    gradle 'gradle6'
  }
}