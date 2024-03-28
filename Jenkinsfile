pipeline {
  agent {
    label 'platform-node'
  }
  
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
    disableConcurrentBuilds()
    timestamps()
  }
  
  tools {
    maven '3.6.3'
    jdk 'openjdk-17.0.2'
  }
  
  environment {
    ARTIFACTORY_CREDENTIALS = credentials('artifactory-access-token')
	ARTIFACTORY_URL = 'http://172.18.173.250/:8082/artifactory/test-app/'
  }
  
  stages {
    stage('Upload Snapshot') {
      steps {
	    sh 'mvn clean install -DskipTests javadoc:jar source:jar-no-fork source:test-jar-no-fork deploy:deploy --batch-mode --settings maven_settings.xml -DaltDeploymentRepository="jfrog-artifactory::${ARTIFACTORY_URL}"'
      }
    }
  }
}