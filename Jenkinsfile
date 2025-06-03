pipeline {
    tools {
        maven"Maven"
    }
    agent any
 
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/Lakshmikdev21/Train-Ticket-Reservation-System.git'
            }
        }
          stage('Build') {
            steps {
               bat 'mvn clean install'
            }
        }
         stage('SonarQube Server') {
            steps {
                bat 'mvn install'
              bat '''mvn sonar:sonar\
  -Dsonar.projectKey=Train-Ticket-Reservation-System \
  -Dsonar.projectName='Train-Ticket-Reservation-System' \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=sqp_cea1ab0998efbcde1a615c1412e144f1a104d2f2'''
            }
        }
          stage('Generate Artifacts') {
            steps {
               archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
            }
        }
		stage('Deploy to Tomcat Server') {
        steps {
            deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'Tomcat', path: '', url: 'http://localhost:8080')], contextPath: 'Train Ticket Reservation System', war: 'target/*.war'
        }
    }
    }
}