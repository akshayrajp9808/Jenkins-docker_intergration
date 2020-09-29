node{
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
        sh 'docker nuild -t akshay9599/akshay-new-app:1.0.0'
    }
}
