pipeline {
    triggers {
  pollSCM('* * * * *')
    }
    agent any
    tools {
  maven 'maven3'
}
   

    stages {
        stage("build & SonarQube analysis") {
            agent {
        docker { image 'maven:3.8.6-openjdk-18' }
    }
            steps {
              withSonarQubeEnv('sonar') {
                sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=kserge2001_geolocation'
              }
            }
          }
         stage('maven analys') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }
          stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
        stage('maven package') {
            steps {
                sh 'mvn clean'
                sh 'mvn install'
                sh 'mvn package'
            }
        }
          stage('test') {
            steps {
               sh 'mvn test'
                
            }
        }
        
         
          stage('deploy') {
            steps {
                echo 'deployement'
                
            }
        }
    }
}
