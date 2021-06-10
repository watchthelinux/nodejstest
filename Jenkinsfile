pipeline {
  agent {
    node {
      label 'test'
    }

  }
  stages {
    stage('Clone Repository for test') {
      steps {
        git(branch: 'master', url: 'https://github.com/watchthelinux/jenkins-npm.git')
      }
    }

    stage('Build configuration on') {
      steps {
        sh 'npm install'
      }
    }

    stage('Deploy on Live through AWX') {
      steps {
        ansibleTower(jobTags: 'Test Deploy', jobTemplate: '9', jobType: 'run', towerCredentialsId: 'f0657fe7-be6c-4527-8810-5a218852c464', towerLogLevel: 'full', towerServer: 'Ansible AWX', verbose: true)
      }
    }

  }
  environment {
    HOME = '.'
  }
}