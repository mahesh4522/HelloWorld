pipeline {
  agent any
 	tools {
        maven 'Maven'
    }
    environment {
    //Use Pipeline Utility Steps plugin to read information from pom.xml into env variables
    pom = readMavenPom file: 'pom.xml'
    VERSION = pom.getVersion()
    }
  	stages {
  	def choice1
    def choice2

    stage ('Select'){
        choice1 = input( id: 'userInput', message: 'Select your choice', parameters: [ [choices: 'aa\nbb', description: '', name: ''] ])
        if(choice1.equals("aa")){
            choice2 = input( id: 'userInput', message: 'Select your choice', parameters: [ [choices: 'yy\nww', description: '', name: ''] ])
        }else{
            choice2 = input( id: 'userInput', message: 'Select your choice', parameters: [ [choices: 'gg\nkk', description: '', name: ''] ])
        }
    }
    stage('Clean, Edit version and Test') { 
            steps {
            	sh "mvn clean"
                sh "sed -i 's/${VERSION}/${params.version}-SNAPSHOT/' pom.xml"
                sh "mvn test"
            }
        }    
  }
}