node{
    agent any
    stage ('scm checkout') {
        git 'https://github.com/spring-petclinic/spring-petclinic-rest.git'
    }
    stage ('Checkout to different branch') {
        sh 'git branch -r'
        sh 'git checkout master'
    }
    stage('Package Stage') {
        sh label: '', script: 'mvn clean package -DSkipTests=true'
    }
    stage('Docker Image Build') {
        sh 'docker build -t akshay9599/akshay-new-app:1.0.0'
    }
    stage('Push Docker Image to DockerHub') {
        withCredentials([string(credentialsId: 'dockerhubaccount', variable: 'dockerhubaccount')]) {
        sh 'docker login -u akshay9599 -p ${dockerhubaccount}'
        }
            sh 'docker push akshay9599/akshay-new-app:1.0.0'
    }
    stage('Deploy to Dev') {
        def dockerRun = 'docker run -d -p 9000:8080 — name my-tomcat-app akshay9599/akshay-new-app:1.0.0'
        sshagent(['deploy-to-dev-docker']) {
            sh 'ssh -o StrictHostKeyChecking=no akshay@192.168.174.148 ${dockerRun}'
        }
    }
}
