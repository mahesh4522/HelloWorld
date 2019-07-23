pipeline {
  agent any
 	tools {
        maven 'Maven'
    }
   parameters {
            choice(
                name: 'isBuildRelease',
                choices:"Yes\nNo",
                description: "Choose Build Type!")
            if(params.isBuilRelease){
               string(
                name: 'version',
                defaultValue:"",
                description: "Input for version number!")
               }
               else{
                return ""
               }
    }
    environment {
    //Use Pipeline Utility Steps plugin to read information from pom.xml into env variables
    pom = readMavenPom file: 'pom.xml'
    VERSION = pom.getVersion()
    }
  	stages {
    stage('Clean, Edit version and Test') { 
            steps {
            	sh "mvn clean"
                sh "sed -i 's/${VERSION}/${params.version}-SNAPSHOT/' pom.xml"
                sh "mvn test"
            }
        }    
  }
}