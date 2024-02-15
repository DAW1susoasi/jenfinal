pipeline {
  agent any
  stages {
    stage('Descargar repositorio') {
      steps {
        sh 'echo "Descargando de repositorio"'
      }
    }

    stage('Ejecutar scritp python') {
      steps {
        sh '~/python-diff.py ./old.xlsx ./new.xlsx'
      }
    }

    stage('Hacer ejecutable script bash') {
      steps {
        sh 'chmod +x meta-script.sh'
      }
    }

    stage('Ejecutar script bash en el servidor') {
      steps {
        sh 'echo "Ejecutando script en el servidor"'
      }
    }

    stage('Crear informe en pdf') {
      steps {
        sh 'pandoc plantilla.md -o informe.pdf'
      }
    }

    stage('Enviar correo con adjunto') {
      steps {
        sh 'echo "Enviando correo"'
      }
    }

    stage('Hacer push a GitHub') {
      steps {
        sh 'echo "Ejecutando script en el servidor"'
      }
    }
  }
  post {
    success {
      sh 'curl -X POST -H "Content-Type: application/json" -d "{\\"chat_id\\": \\"6644496010\\", \\"text\\": \\"Tarea $JOB_NAME OK!! $BUILD_NUMBER,  \\", \\"disable_notification\\": false}" https://api.telegram.org/bot6910914256:AAGPbsMpEj2dEexG8GqgQf_peUSZNBN_O8g/sendMessage'
    }

    failure {
      sh 'curl -X POST -H "Content-Type: application/json" -d "{\\"chat_id\\": \\"6644496010\\", \\"text\\": \\"Falló la tarea $JOB_NAME!! $BUILD_NUMBER,  \\", \\"disable_notification\\": false}" https://api.telegram.org/bot6910914256:AAGPbsMpEj2dEexG8GqgQf_peUSZNBN_O8g/sendMessage'
    }

  }
}
