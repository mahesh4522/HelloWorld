pipeline {
  agent any
 	tools {
        maven 'Maven'
    }
   parameters 
   {
        choice(
       		name: 'Branch',
          	choices:"master",
            description: "Choose branch to build!"
        )
        choice(
       		name: 'isBuildRelease',
          	choices:"Yes/nNo",
            description: "Please choose correct option"
        )
        activeChoiceReactiveReferenceParam('version') {
            description('ActiveChoiceReactiveReferenceParam')
            filterable()
            choiceType('FORMATTED HTML')
            groovyScript {
                			script('''
		 						if (isBuildRelease.equals("Yes")) {
									html='''<input type="text" id = "version" name="value">'''
									return html
								} 
								else{
									return "<b>The version can be automatically set</b>"
								}
					 		''')
					    	fallbackScript('return ["The version can be automatically set!"]')
			}
			referencedParameter('isBuildRelease')
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
                sh "sed -i 's/${VERSION}/${params.version}/' pom.xml"
                sh "mvn test"
            }
        }    
  	}
}