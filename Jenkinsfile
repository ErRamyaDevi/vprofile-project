pipeline {
	agent any
	tools {
		jdk "OracleJDK8"
                maven "MAVEN3.9"
		}
	environment {
		SNAP-REPO = 'devops-snapshots'
                NEXUS-USER = 'admin'
                NEXUS-PASS = 'admin@23'
                RELEASE-REPO = 'devops-release'
                CENTRAL-REPO = 'devops-central'
                NEXUSIP = '172.31.9.243'
                NEXUSPORT = '8081'
                NEXUS-GRP-REPO = 'devops-group'
                NEXUS-LOGIN = 'nexuslogin'
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
