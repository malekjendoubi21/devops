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
                            mvn deploy -DaltDeploymentRepository=${NEXUS_REPO_ID}::default::${NEXUS_URL} \
                                       -DrepositoryId=${NEXUS_REPO_ID} \
                                       -Dnexus.username=${NEXUS_USER} \
                                       -Dnexus.password=${NEXUS_PASS}
                        """
                    }
                }
            }
        }
    }
}
