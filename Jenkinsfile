pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Compiling'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'Testing'
        sh 'mvn test'
      }
    }

    stage('package') {
      steps {
        echo 'Packaging'
        sh 'mvn package -DskipTests=true'
        archiveArtifacts 'target/*.war'
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
}