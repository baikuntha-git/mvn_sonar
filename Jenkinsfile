pipeline {
   agent any
	stages {
      stage('Git Checkout') {
         steps {            
            git 'https://github.com/baikuntha-git/mvn_sonar.git'
		}
	}
	stage('Build Analysis') {
		steps {
			withSonarQubeEnv('sonar') {
				sh '/opt/maven/bin/mvn clean verify sonar:sonar'
			}
		}
	}
	stage("Quality Gate") {
            steps {
              timeout(time: 2, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
	stage ('Deploy') {
		steps {
			sh '/opt/maven/bin/mvn clean install'
		}
	}
}
}
