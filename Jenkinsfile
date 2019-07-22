pipeline {
  agent any
 	tools {
        maven 'Maven'
    }
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
            	sh "cp *.jar ./home/techniche"
                sh "sed -i 's/${VERSION}/${params.version}-SNAPSHOT/' pom.xml"
                sh "mvn test"
            }
        }
        stage('Package') { 
            steps {
                sh "mvn package" 
            }
        }    
  }
}