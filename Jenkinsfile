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
        sh 'echo "Job 06 OK" > job.06.txt'
      }
    }

  }
}