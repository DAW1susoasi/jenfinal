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
        sh '''echo "Ejecutando script python";
        ~/python-diff.py ./old.xlsx ./new.xlsx;'''
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
        script {
          def cuerpoCorreo = "Tarea OK"
          def destinatario = "papi@marchantemeco.duckdns.org"
          def archivoAdjunto = "/home/ubuntu/jenkins_jobs/workspace/06/informe.pdf"
          def asuntoCorreo = "Envío de informe tarea"
          sh "echo \"${cuerpoCorreo}\" | mutt -s \"${asuntoCorreo}\" -a ${archivoAdjunto} -- ${destinatario}"
        }

      }
    }

    stage('Hacer push a GitHub') {
      steps {
        git branch: 'main', url: 'https://github.com/DAW1susoasi/jenfinal.git'
        sh 'git add informe.pdf'
        sh 'git commit -m "Añadir informe.pdf"'
        sh 'git push --set-upstream origin main'
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
