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
nexusArtifactUploader artifacts: [[artifactId: 'maven-jar-plugin', classifier: '', file: 'jar', type: 'jar']], credentialsId: 'NEXUS_CRED', groupId: 'org.apache.maven.plugins', nexusUrl: 'localhost:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-central-repository', version: '3.2.0'
}
}
}
}