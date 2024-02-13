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
        sh '''echo "Haciendo ejecutable script bash";
		chmod +x meta-script.sh;
		// No hace falta copiar el script en el servidor, se ejecuta directamente en el  paso siguiente
		'''
      }
    }
	stage('Ejecutar script bash en el servidor') {
      steps {
        sh '''echo "Ejecutando script en el servidor";
		// ssh ubuntu@marchante.ddns.net 'sudo bash -s' < meta-script.sh;
		'''
      }
    }
	stage('Crear informe en pdf') {
      steps {
        sh '''echo "Creando informe en pdf";
		pandoc plantilla.md -o informe.pdf;'''
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
