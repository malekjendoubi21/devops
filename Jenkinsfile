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

     
        
    }

    post {
        failure {
            echo 'Le build a échoué!'
        }
    }
}
