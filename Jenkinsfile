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

    stage('Run Container on Dev Server') {
      steps {
       sshagent(['ssh206']) {
          sh "ssh -o StrictHostKeyChecking=no dhlee@155.230.25.206 docker run -p 8081:8081 -d dhlee56/ch02tacos"
       }
      }
    }


  }
  tools {
    gradle 'gradle6'
  }
}
