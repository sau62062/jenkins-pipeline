pipeline {
    agent any
    tools {
        maven 'Maven-3.6.3'
    }
    stages {
        stage ('clone the repository') {
            steps {
                git credentialsId: 'Github_User_Password', url: 'https://github.com/sau62062/jenkins-pipeline.git'
            }
        }
        stage ('build the files') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage ('upload the war files') {
            steps {
           nexusArtifactUploader artifacts: [[artifactId: 'Spring3HibernateApp', classifier: '', file: '/var/lib/jenkins/workspace/jenkins pipeline/target/Spring3HibernateApp.war', type: 'war']], credentialsId: 'Nexus_UserName_Password', groupId: 'Spring3HibernateApp', nexusUrl: '3.91.156.52:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOTS'
            }
        }
        stage ('deploy the war file to tomcat') {
            steps {
                deploy adapters: [tomcat7(credentialsId: 'Tomcat_UserName_Password', path: '', url: 'http://3.91.156.52:8080')], contextPath: null, war: '**/*.war'
        }
        }
    }
}
