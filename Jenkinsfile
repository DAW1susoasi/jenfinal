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
	post {
	  success {
		sh 'curl -X POST -H "Content-Type: application/json" -d "{\\"chat_id\\": \\"6644496010\\", \\"text\\": \\"Script python OK!!\\", \\"disable_notification\\": false}" https://api.telegram.org/bot6910914256:AAGPbsMpEj2dEexG8GqgQf_peUSZNBN_O8g/sendMessage'
	  }
	  failure {
		sh 'curl -X POST -H "Content-Type: application/json" -d "{\\"chat_id\\": \\"6644496010\\", \\"text\\": \\"Falló script python\\", \\"disable_notification\\": false}" https://api.telegram.org/bot6910914256:AAGPbsMpEj2dEexG8GqgQf_peUSZNBN_O8g/sendMessage'
	  }
	}
	stage('Copiar script bash en el servidor') {
      steps {
        sh '''echo "Copiando script en el servidor";
		chmod +x meta-script.sh;
        scp -p meta-script.sh marchante.ddns.net:/home/ubuntu/;'''
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
