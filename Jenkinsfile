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
	    sh 'echo "Enviando telegram"'
        // sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "6644496010", "text": "YEEEEEEAAA!!!", "disable_notification": false}\'https://api.telegram.org/bot6910914256:AAGPbsMpEj2dEexG8GqgQf_peUSZNBN_O8g/sendMessage'
      }
    }
    stage('Ejecutar script bash en el servidor') {
      steps {
	    sh 'chmod +x meta-script.sh'
        // sh 'ssh ubuntu@marchante.ddns.net "sudo bash -s" < meta-script.sh'
      }
    }
    stage('Enviar Telegram bash OK') {
      steps {
         sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "6644496010", "text": "YEEEEEEAAA!!!", "disable_notification": false}\'https://api.telegram.org/bot6910914256:AAGPbsMpEj2dEexG8GqgQf_peUSZNBN_O8g/sendMessage'
      }
    }
	  stage('Crear informe en pdf') {
      steps {
        sh 'pandoc plantilla.md -o informe.pdf'
      }
    }
    stage('Hacer push a GitHub') {
      steps {
        sh 'git pull origin main'
        sh 'git add informe.pdf'
        sh 'git commit -m "Añadir informe.pdf"'
        withCredentials([gitUsernamePassword(credentialsId: 'patata', gitToolName: 'Default')]) {
          sh "git push origin HEAD:main"
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