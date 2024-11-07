pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'https://github.com/Ashishkumardevops/gitrepo2', branch: 'main', credentialsId: 'githubuser')
      }
    }

    stage('Build&Publish') {
      steps {
        sh '''sudo docker build -t ashishkumar315/srepo1:latest .
sudo docker push ashishkumar315/srepo1:latest'''
      }
    }

    stage('Deploy') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 7777:80 --name devcon1 ashishkumar315/srepo1:latest


'''
          }
        }

        stage('DeployQA') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 9999:80 --name qacon1 ashishkumar315/srepo1:latest

'''
          }
        }

      }
    }

  }
}