pipeline{
agent any
stages{
stage('Build Application')
step{
   bat 'mvn clean install -MSkipUnittests =true
}
}
stage('deploy Application')
step{
   bat 'mvn package deploy -DmuleDeploy -MSkipUnittests =true
}
}

}