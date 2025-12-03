pipeline {
    agent any

    environment {
        git_branch = 'master'
        git_url = 'git@github.com:maruthibg1998/sBoot.git'
    }

    stages {

        stage('Clone') {
            steps {
                git branch: "${git_branch}", url: "${git_url}"
            }
        }

        stage('Check Java Version') {
            steps {
                sh "java -version"   // Should show Java 1.8.x
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build Project') {
            steps {
                sh 'mvn clean install'
            }
        }
    }
}
