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
    GLOVAL_VAR = 'global variable'
  }
  stages {
    stage('Build'){
      steps {
        echo 'Building'
        echo "$GLOVAL_VAR"
      }
    }
    stage('Test'){
      steps {
        echo 'Testing 2'
      }
    }
    stage('Deploy'){
      steps {
        echo 'Deploy'
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
