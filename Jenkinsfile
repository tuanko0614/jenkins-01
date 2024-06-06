pipeline {
environment {
registry = "tuandt0614/jenkins-01"
registryCredential = 'dockerhub_id'
dockerImage = ''
}
agent any
stages {
stage('Cloning our Git') {
steps {
git url: 'https://github.com/tuanko0614/jenkins-01.git', branch: 'main'
}
}

stage('Start Docker') {
steps{
script {
sh "service docker start"
}
}
}

stage('Building our image') {
steps{
script {
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage('Deploy our image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
stage('Cleaning up') {
steps{
sh "docker rmi $registry:$BUILD_NUMBER"
}
}
}
}