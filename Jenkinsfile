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
        withCredentials(bindings: [usernamePassword(credentialsId: 'githubcred', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
          sh '''
        docker login -u $GIT_USERNAME -p $GIT_PASSWORD
    '''
        }

        sh 'docker push dhlee56/ch02tacos'
      }
    }

    stage('Final Stage') {
      steps {
        echo 'Done'
      }
    }

  }
  tools {
    gradle 'gradle6'
  }
}