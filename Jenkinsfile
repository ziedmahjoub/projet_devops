pipeline {
    agent any

    tools {
        maven 'M2_HOME'
        jdk 'JAVA_HOME'
    }

    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ziedmahjoub/projet_devops.git'
            }
        }
        
       stage('Build') {
    steps {
        sh 'mvn clean package -DskipTests'
    }
}

    }
}
