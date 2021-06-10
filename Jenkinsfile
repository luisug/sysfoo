pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Compile maven app, sysfoo'
        sh 'mvn compile'
        sleep 2
      }
    }

    stage('Test') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Test maven app, sysfoo'
        sh 'mvn clean test'
        sleep 2
      }
    }

    stage('Package') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Package sysfoo app into war file'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.war'
      }
    }

    stage('Docker Build and Publish') {
      agent any
      when {
        branch 'master'
      }
    steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {

            def dockerImage = docker.build("luisug/sysfoo:v${env.BUILD_ID}", "./")

            dockerImage.push()

            dockerImage.push("latest")

          }
        }

      }
    }

stage('Deploy to Dev') {

when {
beforeAgent true
branch 'master'
}

agent any

steps {
echo 'Deploying to Dev Environment with Docker Compose'
sh 'docker-compose up -d'
}
}

  }
  tools {
    maven 'Maven 3.6.3'
  }
}