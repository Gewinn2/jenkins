@Library('myLibrary') _
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
    stage('Test'){
      parallel {
        stage('Linting'){
          steps {
            echo "Linting"
          }
        }
        stage('Unit test'){
          steps {
            echo "Unit testing"
          }
        }
      }
    stage('Build and Deploy') {
      steps {
        docker_build_deploy(
          credentialsId: 'GITLAB_REGISTRY',
          ci_registry: env.CI_REGISTRY,
          image: env.IMAGE_NAME
        )
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
