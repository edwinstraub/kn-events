pipeline {
  agent any
  
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
    disableConcurrentBuilds()
  }
  
  tools {
    maven '3.6.3'
  }
  
  environment {
    ARTIFACTORY_CREDENTIALS = credentials('artifactory-access-token')
	ARTIFACTORY_URL = 'http://172.18.173.250:80/artifactory/test-app/'
  }
  
  stages {
    stage('Upload Snapshot') {
      steps {
	    echo "Credentials: ${ARTIFACTORY_CREDENTIALS}"
		echo "Password: ${ARTIFACTORY_CREDENTIALS_PSW}"
	    sh 'mvn clean install -DskipTests deploy:deploy --batch-mode --settings maven_settings.xml -DaltDeploymentRepository="jfrog-artifactory::default::${ARTIFACTORY_URL}"'
      }
    }
  }
}