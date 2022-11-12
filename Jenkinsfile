pipeline {
    agent {label 'OPEN' }
    parameters {
	string(name: 'GOAL', defaultValue: 'package', description: 'our Goal')
	}
	triggers{
	      pollSCM('* * * * *')
	}
    stages {
        stage ('source code') {
            steps {
                git branch: "dev", 
                    url: "https://github.com/iamsam2772/spring-petclinic-sam.git"
            }
        }
        stage('To build') {
            steps {
                sh "mvn ${params.GOAL}"
            }
        }
        stage("artifact") {
            steps {
                archiveArtifacts "**/target/*.jar"
            }
        }
        stage("junit Reports") {
            steps {
                junit "**/surefire-reports/*.xml"
            }
        }
    }
}
