pipeline {
    agent any

    tools { 
        jdk 'JAVA_HOME' 
        maven 'M2_HOME' 
    }

    environment {
        NEXUS_URL = "http://192.168.56.10:8082/repository/maven-releases/"
        NEXUS_REPO_ID = "nexus"
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

         stage('Deploy to Nexus') {
            steps {
                script {
                    sh """
                    mvn deploy -DaltDeploymentRepository=nexus::default::http://192.168.56.10:8082/repository/maven-releases/
                    """
                }
            }
        }
    }
}
