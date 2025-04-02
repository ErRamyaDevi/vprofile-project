pipeline {
	agent any
	tools {
		      jdk "OracleJDK11"
          maven "MAVEN3.9"
		    }
  environment {
		SNAP_REPO = 'devops-snapshots'
                NEXUS_USER = 'admin'
                NEXUS_PASS = 'ramya@WL123'
                RELEASE_REPO = 'devops-release'
                CENTRAL_REPO = 'devops-central'
                NEXUSIP = '3.18.110.9'
                NEXUSPORT = '8081'
                NEXUS_GRP_REPO = 'devops-group'
                NEXUS_LOGIN = 'nexuslogin'
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
  	}
}
