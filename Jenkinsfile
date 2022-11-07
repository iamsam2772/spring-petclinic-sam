pipeline {
    agent  { label 'openjdk-11-maven' }
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['dev', 'main'], description: 'Branch to build')
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'maven goal')
    }
    stages {
        stage('vcs') {
            steps {
                mail subject: "Build Started for Jenkins JOB $env.JOB_NAME", 
                  body: "Build Started for Jenkins JOB $env.JOB_NAME", 
                  to: 'masameer9440@gmail.com' 
                git branch: "${params.BRANCH_TO_BUILD}"
				, url: 'https://github.com/iamsam2772/spring-petclinic-sam.git'
            }
            
        }
        stage('build') {
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }
        
    }
    post {
        always {
            echo 'Job completed'
            mail subject: "Build Completed for Jenkins JOB $env.JOB_NAME", 
                  body: "Build Completed for Jenkins JOB $env.JOB_NAME \n Click Here: $env.JOB_URL", 
                  to: 'masameer9440@gmail.com'
        }
        failure {
            mail subject: "Build Failed for Jenkins JOB $env.JOB_NAME with Build ID $env.BUILD_ID", 
                  body: "Build Failed for Jenkins JOB $env.JOB_NAME", 
                  to: 'masameer9440@gmail.com' 
        }
        success {
            junit '**/surefire-reports/*.xml'
        }
    }
}