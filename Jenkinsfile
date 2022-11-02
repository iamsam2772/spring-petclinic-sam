pipeline {
    agent {label 'OPEN' }
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['rel', 'dev', 'main'], description: 'Branch to build')
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'maven goal')

    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage ('source code  from git remote repository') {
            steps {
                git branch: "${params.BRANCH_TO_BUILD}", url: 'https://github.com/iamsam2772/spring-petclinic-sam.git'
            }
        }
        stage('To build maven package') {
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
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