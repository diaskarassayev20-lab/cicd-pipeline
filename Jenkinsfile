pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh './scripts/test.sh'
      }
    }

    stage('Docker Publish') {
      steps {
        script {
          def dockerImage = docker.build("$registry")
          docker.withRegistry('', "$registryCredential"){
            dockerImage.push()
            dockerImage.push("latest")
          }
        }

      }
    }

  }
  environment {
    registry = 'diaskarassayev20-lab/cicd-pipeline'
    registryCredential = 'diaskarassayev20'
  }
}