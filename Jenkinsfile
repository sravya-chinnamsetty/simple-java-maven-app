pipeline {
agent any



tools{
maven "maven3"
}



stages {

stage('Hello') {
steps {
echo 'Hello World'
}
}


stage('Build') {
steps {

checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'githubcredentials', url: 'https://github.com/sravya-chinnamsetty/simple-java-maven-app.git']]])
bat 'mvn -B -DskipTests clean package'
}
}
stage('Test') {
steps {

bat 'mvn test -Dmaven.test.failure.ignore=true'
}
}
stage('sonar') {
steps {

bat 'mvn sonar:sonar -Dsonar.login=857993ae03a96b3c557f21977fa10bc2a83e439d'
}
}
stage('nexus') {
steps {

nexusArtifactUploader artifacts: [[artifactId: 'pom.my-app', classifier: '', file: 'pom.xml', type: 'pom']], credentialsId: 'NEXUS_CRED', groupId: 'pom.com.mycompany.app', nexusUrl: 'localhost:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-central-repository', version: 'pom.1.0-SNAPSHOT'
}
}
}
}