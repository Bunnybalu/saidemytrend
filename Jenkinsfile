pipeline {
    agent any
	environment {
		PATH = "/opt/maven/bin:$PATH"
	
	stages {
	  stage ("build") {
	   steps {
		sh 'mvn clean deploy'
		}
	}
	stage ("SonarQube analysis") {
		environment {
			scannerHome = tool 'saidemy-sonarQube-scanner'
	   }
	    steps {
		with SonarQubeEnv('saidemy-sonarQube-scanner') {
			sh "${scannerHome}/bin/sonar-scanner"
		}
	}
   }
  }
 }

