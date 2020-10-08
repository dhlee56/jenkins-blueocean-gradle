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
        script {
          sshagent(['dev-server'])

          {
            sh "ssh -o StrictHostKeyChecking=no dhlee@155.230.16.19 docker run -p 8081:8081 -d --name my-app dhlee56/ch02tacos"
          }
        }

      }
    }

  }
  tools {
    gradle 'gradle6'
  }
}