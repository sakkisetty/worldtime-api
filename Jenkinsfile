pipeline {
  agent any
  stages {
    stage('Build Application') { 
      steps {
        bat 'mvn clean install'
      }
    }
    stage('Upload  to Nexus repository') { 
      steps {
        bat 'mvn clean deploy'
      }
    }
      stage('Deploy Application to Cloudhub') { 
      steps {
        bat 'mvn clean package deploy -DmuleDeploy'
      }
    }
  }
}