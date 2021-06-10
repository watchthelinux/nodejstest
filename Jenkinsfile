pipeline {
    agent {
        docker {
            image 'nodetest:latest' 
            args '-p 3000:3000' 
        }
    }
        environment {
        HOME = '.'
        }
    stages {
        stage('Clone Repository for test') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/watchthelinux/jenkins-npm.git'
            }
        }
        stage('Build configuration on') { 
            steps {
                sh 'npm install' 
            }
        }
        stage('Deploy on Live through AWX') {
            steps {
                 ansibleTower jobTags: 'Test Deploy', jobTemplate: '9', jobType: 'run', throwExceptionWhenFail: false, towerCredentialsId: 'f0657fe7-be6c-4527-8810-5a218852c464', towerLogLevel: 'full', towerServer: 'Ansible AWX', verbose: true          
            }   
        }
    }
}
