pipeline {
    agent any

    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    stages {

        stage("Build") {
            steps {
		 echo "build started"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
		 echo "build completed"
            }

        }
	stage ("test") { 
	    steps {
			echo "unit test started"
			sh 'mvn surefire_report:report'
			echo "unit test completed"
		}
	}
        stage("SonarQube analysis") {
            environment {
                scannerHome = tool 'saidemy-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('saidemy-sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }

    }
}
