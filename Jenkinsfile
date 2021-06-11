pipeline {
    agent {
        docker {
            image 'nodetest:latest' 
            args '-p 3000:3000' 
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
        ansibleTower credential: '8', inventory: 'jenkinstestmachine115l', jobTemplate: '13', jobType: 'run', throwExceptionWhenFail: false, towerCredentialsId: 'af774254-7d1e-41de-904c-682857dbd8ef', towerLogLevel: 'full', towerServer: 'Ansible AWX'
      }
    }

  }
  environment {
    HOME = '.'
  }
}
