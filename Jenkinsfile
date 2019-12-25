pipeline {
  agent any
  stages {
    stage('Build Application') { 
      steps {
        bat 'mvn clean install'
      }
    }
      stage('Deploy Application') { 
      steps {
        bat 'mvn package deploy -DmuleDeploy'
      }
    }
  }
}