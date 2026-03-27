pipeline {
    agent any
    tools {
        maven "maven3.9"
        jdk "jdk17"
    }
    
    environment {
        SNAP_REPO = 'vprofile-snapshot'
		NEXUS_USER = 'admin'
		NEXUS_PASS = 'admin123'
		RELEASE_REPO = 'vprofile-release'
		CENTRAL_REPO = 'vpro-maven-central'
		NEXUSIP = '172.31.27.140'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post{
                success{
                    echo "Now Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }

            }
        }
        stage('Test'){
            steps {
                sh 'mvn test'
            }
        }
        stage('Checkstyle Analysis'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }
         
    }
}