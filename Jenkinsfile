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
    stage('Enviar Telegram python OK') {
      steps {
        // sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "6644496010", "text": "YEEEEEEAAA!!!", "disable_notification": false}\'https://api.telegram.org/bot6910914256:AAGPbsMpEj2dEexG8GqgQf_peUSZNBN_O8g/sendMessage'
      }
    }
    stage('Ejecutar script bash en el servidor') {
      steps {
<<<<<<< HEAD
	    sh 'chmod +x meta-script.sh'
        // sh 'ssh ubuntu@marchante.ddns.net "sudo bash -s" < meta-script.sh'
=======

>>>>>>> 66a1894fd27c321abe9c4751dd4178aca59973ba
      }
    }
    stage('Enviar Telegram bash OK') {
      steps {
         sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "6644496010", "text": "YEEEEEEAAA!!!", "disable_notification": false}\'https://api.telegram.org/bot6910914256:AAGPbsMpEj2dEexG8GqgQf_peUSZNBN_O8g/sendMessage'
      }
    }
	  stage('Crear informe en pdf') {
      steps {
<<<<<<< HEAD
        sh 'pandoc plantilla.md -o informe.pdf'
=======
        script {

        }
>>>>>>> 66a1894fd27c321abe9c4751dd4178aca59973ba
      }
    }
    stage('Hacer push a GitHub') {
      steps {

        }
      }
    }
  }
  post {
    success {
      script {
	    def cuerpoCorreo = "Tarea OK"
	    def destinatario = "papi@marchantemeco.duckdns.org"
	    def archivoAdjunto = "/home/ubuntu/jenkins_jobs/workspace/06/informe.pdf"
	    def asuntoCorreo = "Envío de informe tarea"
	    sh "echo \"${cuerpoCorreo}\" | mutt -s \"${asuntoCorreo}\" -a ${archivoAdjunto} -- ${destinatario}"
	  }
    }
    failure {
      sh 'curl -X POST -H "Content-Type: application/json" -d "{\\"chat_id\\": \\"6644496010\\", \\"text\\": \\"Falló la tarea $JOB_NAME!! $BUILD_NUMBER  \\", \\"disable_notification\\": false}" https://api.telegram.org/bot6910914256:AAGPbsMpEj2dEexG8GqgQf_peUSZNBN_O8g/sendMessage'
    }
  }
}