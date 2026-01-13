pipeline {
  agent any
  environment {
      APP_NAME = "my-node-app"
      DEPLOY_PORT = 3000
      }
  tools {
   nodejs "NodeJS_25"
      }
      stages{
      stage('Checkout Code'){
       steps {
        echo 'Checking out code from this repository'
	 checkout scm
       }
      }
      stage('Install Dependencies') {
       steps {
        sh 'npm install'
       }
      }
      stage('Build Application') {
       steps {
         sh 'npm run build || echo "no build script found, skipping build."'
       }
      }
      stage('Run Application Locally') {
       steps {
         script {
	  sh 'pkill -f "node app.js" || true'
	  sh 'nohup node app.js > app.log 2>&1 &'
	  sleep(time:5, unit: 'SECONDS')
	  }
	  }
	  }
	  }
	  post {
	  always {
	  sh 'pkill -f "node app.js" || true'
	  archiveArtifacts artifacts; 'app.log' allowEmptyArchive:true
	  }
	  success {
	   echo 'Build and local deployment succeeded'
	  }
	  failure {
	   echo 'Build or deployment failed'
	   }
	   }
	   }


