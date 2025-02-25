
pipeline {
    agent any

    tools { 
        jdk 'JAVA_HOME' 
        maven 'M2_HOME' 
    }

    stages {
        stage('GIT') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/malekjendoubi21/devops.git'
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
                                 mvn deploy -DaltDeploymentRepository=nexus::default::http://your-nexus-server:8081/#browse/browse:maven-releases/ \
                                            -DrepositoryId=nexus \
                                            -Dnexus.username=${NEXUS_USER} \
                                            -Dnexus.password=${NEXUS_PASS}
                                 """
                             }
                         }
                     }
          }

        

}
}
