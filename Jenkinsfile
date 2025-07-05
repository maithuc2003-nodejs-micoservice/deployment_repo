pipeline {
  agent any

  environment {
    COMPOSE_PROJECT_NAME = 'fashion_stack'
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
            bat "docker-compose --env-file %ENV_PATH% -f docker-compose.yml down"
            bat "docker-compose --env-file %ENV_PATH% -f docker-compose.yml up -d --remove-orphans"
          }
        }
      }
    }
  }
//  configFileProvider([configFile(fileId: 'env_user_service', targetLocation: '.env')]) {
//           bat '''
//             docker-compose --env-file .env pull
//             docker-compose --env-file .env up -d --remove-orphans
//           '''

  post {
    success {
      echo "✅ Docker Compose started successfully"
    }
    failure {
      echo "❌ Docker Compose failed"
    }
  }
}
