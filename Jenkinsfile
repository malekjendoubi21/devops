pipeline {
    agent any

    tools { 
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

    stages {
        stage('GIT') {
            steps {
                git branch: 'master', url: 'https://github.com/malekjendoubi21/devops.git'
            }
        }

        stage('Compile Stage') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn package'
                sh 'mvn test'
            }
        }
    }

    post {
        failure {
            echo 'Le build a échoué!'
        }
    }
}
