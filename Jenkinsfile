pipeline {
  agent {
    docker {
      args '''-p 3000:3000
'''
      image 'node:18-alpine'
    }

  }
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
          docker.withRegistry('', registryCredential){
            dockerImage.push()
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