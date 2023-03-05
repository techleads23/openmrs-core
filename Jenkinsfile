pipeline {
        agent { label 'JDK8' }
        stages {
                stage('SourceCode') {
                    steps {
                         git branch: 'master', url: 'https://github.com/techleads23/openmrs-core.git'
                }
            }
                stage('Build the code and sonar analysis') {
                    steps {
                         withSonarQubeEnv('SONAR_LATEST') { 
                         sh 'mvn clean package sonar:sonar'
                       }
                   }
                }
                stage ('Archiving and Test Results') {
                    steps {
                }
            }
        }
   }
