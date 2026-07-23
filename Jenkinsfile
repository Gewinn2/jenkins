pipeline {
  agent any
  // triggers { pollSCM('* * * * *') }
  options {
    disableConcurrentBuilds() // Запрет одновременных сборок
    timestamps() // Вывод времени выполнения шагов в логах
    timeout(time: 1, unit: 'HOURS') // Максимальное время выполнения пайплайна
    buildDiscarder(logRotator(artifactDaysToKeepStr: '7', artifactNumToKeepStr: '10', daysToKeepStr: '7', numToKeepStr: '10')) // Сколько дней хранится артефакт, сколько артефактов хранить, сколько дней хранить логи сборок, сколько последних сборок хранить
  }
  environment {
    CI_REGISTRY = credentials('CI_REGISTRY')
    IMAGE_NAME = 'gl-registry.gewinn2-pet.ru/demo-group/demo-project/hello_app:latest'
  }
  stages {
    stage('Login'){
      steps {
        withCredentials([usernamePassword(credentialsId: 'GITLAB_REGISTRY', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
          sh '''
            echo "$PASSWORD" | docker login -u $USER --password-stdin "$CI_REGISTRY"
          '''
        }
      }
    }
    stage('Build'){
      steps {
        sh 'docker build -t $IMAGE_NAME .'
        sh 'docker push $IMAGE_NAME'
      }
    }
    stage('Deploy'){
      steps {
        echo 'Deploy 2'
      }
    }
  }
  post {
    always {
      echo 'Pipeline finished'
    }
    success {
      echo 'successfully'
    }
    failure {
      echo 'failed'
    }
  }
}
