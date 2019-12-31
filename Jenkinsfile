pipeline {
  agent any
  node {
    // define the secrets and the env variables
    // engine version can be defined on secret, job, folder or global.
    // the default is engine version 2 unless otherwise specified globally.
    def secrets = [
        [path: 'secret/testing', engineVersion: 1, secretValues: [
            [envVar: 'testing', vaultKey: 'value_one'],
            [envVar: 'testing_again', vaultKey: 'value_two']]],
        [path: 'secret/another_test', engineVersion: 2, secretValues: [
            [vaultKey: 'another_test']]]
    ]

    // optional configuration, if you do not provide this the next higher configuration
    // (e.g. folder or global) will be used
    def configuration = [vaultUrl: 'http://http://127.0.0.1:8200/',
                         vaultCredentialId: 'my-vault-cred-id',
                         engineVersion: 1]
    // inside this block your credentials will be available as env variables
    withVault([configuration: configuration, vaultSecrets: secrets]) {
        sh 'echo $testing'
        sh 'echo $testing_again'
        sh 'echo $another_test'
    }
}
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
      stage('Run Performance tests') { 
      steps {
        bat 'newman run C:\\Mulesoft\\studio-workspace\\worldtime-api\\WorldTime.postman_collection.json -r htmlextra'
      }
    }
  }
}