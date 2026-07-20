pipeline {
  agent any
  options {
    ansiColor('xterm')
    disableConcurrentBuilds() // Запрет одновременных сборок
    timestamps() // Вывод времени выполнения шагов в логах
    timeout(time: 1, unit: 'HOURS') // Максимальное время выполнения пайплайна
    buildDiscarder(logRotator(artifactDaysToKeepStr: '7', artifactNumToKeepStr: '10', daysToKeepStr: '7', numToKeepStr: '10')) // Сколько дней хранится артефакт, сколько артефактов хранить, сколько дней хранить логи сборок, сколько последних сборок хранить
  }
  stages {
    stage('Build'){
      steps {
        echo 'Building'
      }
    }
    stage('Test'){
      steps {
        echo 'Testing'
      }
    }
    stage('Deploy'){
      steps {
        echo 'Deploy'
      }
    }
  }
}
