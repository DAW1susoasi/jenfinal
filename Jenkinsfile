pipeline {
  agent any
  stages {
    stage('primer') {
      steps {
        sh 'echo "Descargando users-240123.xlsx de repositorio"'
      }
    }

    stage('segun') {
      steps {
        sh '''echo "Ejecutando script python";
        ~/python-diff.py ~/users-240122.xlsx ./users-240123.xlsx;'''
      }
    }

  }
}
