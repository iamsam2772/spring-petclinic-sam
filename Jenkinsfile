pipeline {
    agent {label 'OPEN' }
    parameters {
	choice(name: 'BRANCH', choices: ['main', 'dev', 'rel'], description: 'select branch to build')
	string(name: 'GOAL', defaultValue: 'package', description: 'our Goal')
	}
	triggers{
	      pollSCM('* * * * *')
	}
    stages {
        stage ('source code  from git remote repository') {
            steps {
                git branch: "${params.BRANCH}", url: 'https://github.com/iamsam2772/spring-petclinic-sam.git'
            }
        }
        stage('To build maven package') {
            steps {
                sh "mvn ${params.GOAL}"
            }
        }
        stage("archive artifact") {
            steps {
                archiveArtifacts '**/target/*.jar'
            }
        }
        stage("junit Reports") {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
    }
}
