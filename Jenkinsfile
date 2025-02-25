pipeline {
    agent any

    tools { 
        jdk 'JAVA_HOME' 
        maven 'M2_HOME' 
    }

    environment {
        NEXUS_URL = "http://192.168.56.10:8081/repository/maven-releases/"
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
                    withCredentials([usernamePassword(credentialsId: 'nexus', usernameVariable: 'NEXUS_USER', passwordVariable: 'NEXUS_PASS')]) {
                        sh """
                          mvn clean package deploy:deploy-file \
    -Dfile=target/timesheet-devops-1.0.jar \
    -Durl=http://192.168.56.10:8081/repository/maven-releases/ \
    -DrepositoryId=nexus \
    -DgroupId=tn.esprit.spring.services \
    -DartifactId=timesheet-devops \
    -Dversion=1.0

                        """
                    }
                }
            }
        }
    }
}
