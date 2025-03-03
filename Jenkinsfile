pipeline {
	agent any
	tools {
		jdk "JDK21"
                maven "MAVEN3.9"
		}
	environment {
		SNAP_REPO = 'devops-snapshots'
                NEXUS_USER = 'admin'
                NEXUS_PASS = 'admin@23'
                RELEASE_REPO = 'devops-release'
                CENTRAL_REPO = 'devops-central'
                NEXUSIP = '172.31.9.243'
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
