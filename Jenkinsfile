pipeline {
  agent any
  tools {
    jfrog 'jfrog-cli-latest'
  }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
	  ARTIFACTORY_URL = 'http://172.18.173.250/:8082/artifactory/'
	  ARTIFACTORY_REPO_ID = 'test-app/'
  }
  stages {
    stage('Build') {
      steps {
	    sh 'chmod +x mvnw'
        sh './mvnw clean install -DskipTests'
      }
    }
    stage('Upload to Artifactory') {
      steps {
	    jf '-v'
		jf 'rt ping'
        jf 'rt upload --url ${ARTIFACTORY_URL} --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/eventing-1.0.0-SNAPSHOT.jar ${ARTIFACTORY_REPO_ID}'
      }
    }
	
	post {
	  always {
	    cleanWs()
	  }
	}
  }
}