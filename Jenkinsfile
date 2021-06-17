pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'complie sysfoo app'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'test maven app'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      steps {
        echo 'package maven app'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.war'
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
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}
