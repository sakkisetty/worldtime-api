pipeline{
agent any
stages{
stage('Build Application')
step{
   bat 'mvn clean install'
}
}
stage('deploy Application')
step{
   bat 'mvn package deploy -DmuleDeploy'
}
}

}