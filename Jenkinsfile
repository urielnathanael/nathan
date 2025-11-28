// Jenkinsfile
pipeline {
  agent any
  environment {
    // Optionnel : forcer le workspace comme base pour docker compose si besoin
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build & Deploy (docker-compose)') {
      steps {
        // Affiche contexte
        sh 'echo "Workspace: $WORKSPACE"'
        // Lancer docker compose (sur la VM via socket monté)
        sh 'docker compose -f docker-compose.yml up -d --build'
      }
    }
    stage('Smoke test') {
      steps {
        // Simple vérif : requête HTTP vers le service local (depuis la VM)
        sh 'sleep 2'
        sh 'curl -f http://localhost:8081 || (echo "Site non joignable"; exit 1)'
      }
    }
  }
  post {
    success {
      echo 'Déploiement réussi.'
    }
    failure {
      echo 'Echec. Voir logs.'
    }
  }
}
