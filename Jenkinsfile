pipeline {
  agent any
  stages {
    stage('Unit Test') { 
      steps {
        bat 'mvn clean install'
      }
    }
  }
}