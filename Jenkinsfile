pipeline {
     agent { label 'JDK8' }
     options { 
	timeout(time: 1, unit: 'HOURS')
        retry(2)
       }
     triggers {
	cron('0 * * * *')
     }
     parameters {
          choice(name: 'GOAL',choices: ['compile', 'package', 'clean package'])
      }
    stages {
    	stage('Source code') {
          steps {
	     git url: 'https://github.com/techleads23/openmrs-core.git',branch: 'master'
	}
      }
        stage('Build the code and Sonar Cube Analysis') {
          steps {
                withSonarQubeEnv('SONAR_LATEST') { 
	         sh script: 'mvn clean package sonar:sonar' 	
            }
          }
	}
	stage('Reporting and Archiving') {
 	  steps {
            junit testResults: 'target/surefire-reports/*.xml'
	}
      }
   }
   post {
       success {
        //send the success email
        echo "Success"
   }
       unsuccessful{
	//send the unsuccess email
        echo "Failure"
      }

    }  
}
