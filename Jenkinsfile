pipeline {
  agent any
   environment {
        SECRET = vault path: 'secrets/nexuspath', key: 'url', engineVersion: "2"
    }
  stages {
   stage("read vault key") {
            steps {
                echo "${SECRET}"
            }
        }
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
      stage('Run Performance tests') { 
      steps {
        bat 'newman run C:\\Mulesoft\\studio-workspace\\worldtime-api\\WorldTime.postman_collection.json -r htmlextra'
      }
    }
  }
}