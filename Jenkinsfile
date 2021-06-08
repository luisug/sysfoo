pipeline {
  agent {
    docker {
      image 'maven:3.6.3-jdk-11-slim'
    }

  }
  stages {
    stage('Build') {
      steps {
        echo 'Compile maven app, sysfoo'
        sh 'mvn compile'
        sleep 2
      }
    }

    stage('Test') {
      steps {
        echo 'Test maven app, sysfoo'
        sh 'mvn clean test'
        sleep 2
      }
    }

    stage('Package') {
      steps {
        echo 'Package sysfoo app into war file'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.war'
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
}