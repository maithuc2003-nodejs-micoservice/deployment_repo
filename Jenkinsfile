pipeline {
  agent any

  environment {
    COMPOSE_PROJECT_NAME = 'fashion_web'
  }

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/maithuc2003-nodejs-micoservice/deployment_repo.git', branch: 'main'
      }
    }
// https://github.com/maithuc2003-nodejs-micoservice/deployment_repo.git
    stage('Use Secret .env') {
      steps {
        withCredentials([file(credentialsId: 'ENV_FILE_KLTN_NODEJS', variable: 'ENV_PATH')]) {
          script {
            bat "docker-compose --env-file %ENV_PATH% -f docker-compose.yml down -v --remove-orphans"
            bat "docker-compose --env-file %ENV_PATH% -f docker-compose.yml up -d --build"
          }
        }
      }
    }
  }
  post {
    success {
      echo "✅ Docker Compose started successfully"
    }
    failure {
      echo "❌ Docker Compose failed"
    }
  }
}
