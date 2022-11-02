pipeline {
    agent {label 'OPEN' }
	stages {
        stage ('source code  from git remote repository') {
            steps {
                git branch: 'main', url: 'https://github.com/iamsam2772/spring-petclinic-sam.git'
            }
        }
        stage('To build maven package') {
            steps {
                sh "mvn package"
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