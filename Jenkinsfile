pipeline {
    agent any

    tools {
        jdk 'JAVA_HOME'    // Ensure this matches the configured name in Jenkins
        maven 'M2_HOME'    // Ensure this matches the configured name in Jenkins
    }

    stages {
        stage('GIT') {
            steps {
                git branch: 'master', url: 'https://github.com/malekjendoubi21/devops.git'
            }
        }
        stage('Compile Stage') {
            steps {
                // For Linux or Unix-based agents
              //  sh 'mvn clean compile'

                // For Windows-based agents (use only one of these, depending on your environment)
                 bat 'mvn clean compile'
            }
        }
    }

    post {
        failure {
            echo 'Le build a échoué!'
        }
    }
}
