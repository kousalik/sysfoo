pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }
      }
      steps {
        echo 'Compiling'
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }
      }
      steps {
        echo 'Testing'
        sh 'mvn test'
      }
    }

    stage('package') {
      when {
        branch 'master'
      }
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }
      }
      steps {
        echo 'Packaging'
        sh 'mvn package -DskipTests=true'
        archiveArtifacts 'target/*.war'
      }
    }
    stage('Docker BnP') {
      when {
          branch 'master'
      }
      agent any
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
            def dockerImage = docker.build("kousalix/sysfoo:v${env.BUILD_ID}", './')
            dockerImage.push()
            dockerImage.push('latest')
          }
        }
      }
    }
  }
  tools {
    maven 'Maven 3.6.3'
  }
}
