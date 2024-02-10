pipeline {
  agent any
  stages {
    stage('primer') {
      steps {
        sh 'ls -l /python'
      }
    }

    stage('segun') {
      steps {
        sh 'cp ./users-240122.xlsx /python; ls -l /python'
      }
    }

  }
}