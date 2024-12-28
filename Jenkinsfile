pipeline {
  agent any
  tools{
    maven 'sonarmaven'
  }
  environment {
    SONAR_TOKEN =credentials('sonar-token')
  }
stages{
  stage('Checkout'){
    steps{
      checkout scm
    }
  }
  stage('Build'){
    steps {
      bat 'mvn clean package'
    }
  }
  stage('SonarQube Analysis'){
    steps{
      withSonarQubeEnv('sonarqube'){
        bat"""
        mvn clean verify sonar:sonar \
        -Dsonar.projectKey=sonarmaven2 \
        -Dsonar.projectName='sonarmaven2' \
        -Dsonar.host.url=http://localhost:9000 \
        -Dsonar.token=sqp_506dda3c0f74f428a787bf9d9835500a8ebbf011
        """
      }
    }
  }
}
  post {
    success {
      echo 'Pipeline completed successfully.'
    }
    failure{
      echo 'pipeline failed'
    }
  }
}
        
