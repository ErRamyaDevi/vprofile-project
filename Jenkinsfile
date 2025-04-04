pipeline {
	agent any
	tools {
		      jdk "OracleJDK8"
         		maven "MAVEN3.9"
		    }
  environment {
		SNAP_REPO = 'devops-snapshots'
                NEXUS_USER = 'admin'
                NEXUS_PASS = 'ramya@WL123'
                RELEASE_REPO = 'devops-release'
                CENTRAL_REPO = 'devops-central'
                NEXUSIP = '18.219.110.109'
                NEXUSPORT = '8081'
                NEXUS_GRP_REPO = 'devops-group'
                NEXUS_LOGIN = 'nexuslogin'
	  	SONARSERVER = 'sonarserver'
        	SONARSCANNER = 'sonarscanner'
		}
  stages{
  		stage('BUILD'){
  			steps {
  				sh 'mvn -s settings.xml -DskipTests install'
  				}
			post {
				success {
					echo "Archiving"
					archiveArtifacts artifacts: '**/*.war'
						}
				}
  		}
	  	stage('Test') {
			steps {
				sh 'mvn -s settings.xml test'
			}
		}
	  	stage('Checkstyle Analysis') {
			steps {
				sh 'mvn -s settings.xml checkstyle:checkstyle'
			}
		}
	  	stage('Sonar Analysis') {
           		 environment {
                	scannerHome = tool "${SONARSCANNER}"
           	 		}
		            steps {
		               withSonarQubeEnv("${SONARSERVER}") {
		                   sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
		                   -Dsonar.projectName=vprofile \
		                   -Dsonar.projectVersion=1.0 \
		                   -Dsonar.sources=src/ \
		                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
		                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
		                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
		                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
		              	}
		            }
      		  }
  	}
}
