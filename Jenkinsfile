pipeline {
  agent any
   parameters {
        string(name:'version',
        defaultValue:'',
        description:'')
    }
    environment {
    //Use Pipeline Utility Steps plugin to read information from pom.xml into env variables
    pom = readMavenPom file: 'pom.xml'
    VERSION = pom.getVersion()
    }
  	stages {
    stage('Clean, Edit version and Test') { 
            steps {
                sh "sed -i 's/VERSION/${params.version}/' pom.xml"
                sh "mvn test -f HelloWorld"
            }
        }
        stage('Package') { 
            steps {
                sh "mvn package -f HelloWorld" 
            }
        }    
  }
}