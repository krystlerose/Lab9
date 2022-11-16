pipeline {
	agent any
	stages {
		stage ('Checkout') {
			steps {
				git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
			}
		}
		stage('Code Quality Check via SonarQube') {
			steps {
				script {
					def scannerHome = tool 'SonarQube';
					withSonarQubeEnv('SonarQube') { 
						sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://172.18.0.4:9000 -Dsonar.login=sqp_0d07b962f997ac0b24398e5ad98afaf9763fac8b"
					}
				}
			}
		}
	}
	post {
		always {
			recordIssues enabledForFailure: true, tool: sonarQube()
		}
	}
}
