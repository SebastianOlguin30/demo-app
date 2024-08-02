pipeline {
    agent any

    tools {
        maven 'Default Maven' // Asegúrate de que 'Default Maven' está configurado en Jenkins
    }

    stages {
        stage('SCM') {
            steps {
                // El checkout debe estar dentro de un bloque steps
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            def mvn = tool 'Default Maven';
            withSonarQubeEnv() {
            sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=Sonar_Jenkinsfile -Dsonar.projectName='Sonar_Jenkinsfile'"
            }

            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // Aquí puedes agregar tus comandos de compilación, por ejemplo:
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Aquí puedes agregar tus comandos de prueba, por ejemplo:
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Aquí puedes agregar tus comandos de despliegue, por ejemplo:
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
