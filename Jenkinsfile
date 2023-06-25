pipeline {
    agent any
    tools{
        maven 'maven-3.9.2'
    }
    stages {
        stage('Clone Repo') {
            steps {
                // Clone the git repo
                echo 'This is stage 1'
                git 'https://github.com/salihonder/DevOpsClassCodes.git'
            }
        }
        stage('Compile') {
            steps {
                echo 'This is stage 2'
                sh 'mvn compile'
            }
        }
        stage('Code Review') {
            steps {
                echo 'This is stage 3'
                sh 'mvn pmd:pmd'
            }
            post{
                success{
                    recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')])
                }
            }
        }
        
         stage('Code Test') {
            steps {
                echo 'This is stage 4'
                sh 'mvn test'
            }
            post{
                success{
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }
}
