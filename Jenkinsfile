pipeline {
    agent any
tools{
    maven "Maven-3.6.3"
}
    stages {
        stage('Clone the Project') {
            steps {
                git branch: 'murali', changelog: false, credentialsId: 'git_username_password', poll: false, url: 'https://github.com/MooleMuraliDharaReddy/java-app.git'
            }
        }
        stage('Build the project'){
            steps{
                
                sh 'mvn clean install'
                
            }
        }
        stage('Upload the artifacts'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'Spring3HibernateApp', classifier: '', file: '/var/lib/jenkins/workspace/jenkins-pipeline-project/target/Spring3HibernateApp.war', type: 'war']], credentialsId: 'Nexus_username_password', groupId: 'Spring3HibernateApp', nexusUrl: '3.236.45.152:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
            }
        }
        stage ('DEV Deploy') {
      steps {
      echo "deploying to DEV Env "
     deploy adapters: [tomcat7(credentialsId: 'tomcat_username_password', path: '', url: 'http://3.236.45.152:8080/')], contextPath: null, war: '**/*.war'    
          
          
      }
    }
    
     stage ('DEV Approve') {
      steps {
      echo "Taking approval from DEV Manager for QA Deployment"
        timeout(time: 7, unit: 'DAYS') {
        input message: 'Do you want to deploy?', submitter: 'admin'
		
		
        }
      }
    }
    }
}
