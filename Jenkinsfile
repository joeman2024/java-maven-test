pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Build success'
                    archiveArtifacts artifacts: '**/target/*.war', 
                }
                failure {
                    echo 'Build failed'
                }
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                echo 'Deploying the project...'
                deploy adapters: [tomcat9(credentialsId: 'tomcatserver', path: '', url: 'http://3.129.87.121:8080/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
