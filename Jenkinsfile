pipeline {
    agent {label 'openjdk-11-maven'}
    stages {
        stage ('source code  from git remote repository') {
            steps {
               git url: 'https://github.com/iamsam2772/spring-petclinic-sam.git',
                branch: 'main'
            }
        }
        stage ('Artifactory configuration') {
            steps {
				rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId:     "jfrog_masameer",
                    releaseRepo:  "qt-libs-release-local",
                    snapshotRepo: "qt-libs-snapshot-local",
                    deployArtifacts : true
                )
            }
        }
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool:  "MVN_DEFAULT",
                    pom:   "pom.xml",
                    goals: "clean install",
                    deployerId: "MAVEN_DEPLOYER",
                )
            }
        }
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "jfrog_masameer"
                )
            }
        }
    }	
}