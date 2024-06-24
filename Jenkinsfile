pipeline {
    agent any
    tools {
        maven 'maven1'
    }
    environment {
        dockerversion = 'karunasulakhe/addressbook:1.${env.BUILD_NUMBER}'
    }
    stages {
        stage('checkout') {
            steps {
                git 'https://github.com/niladrimondal/addressbook-demo.git'
            }
        }
        stage('build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('create docker image') {
            steps {
                sh 'docker build -t kavyasulakhe/addressbook:1.${BUILD_NUMBER} .'
            }
        }
         stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerpwd', usernameVariable: 'dockeruser')]) {
          sh "docker login -u ${env.dockeruser} -p ${env.dockerpwd}"
          sh 'docker push kavyasulakhe/addressbook:1.${BUILD_NUMBER}'
        }
      }
    }

    }
}
