pipeline {
  agent any
  stages {
    stage('pull-repo') {
      steps {
        git(url: 'https://github.com/hakxcore/assignment', branch: 'main')
      }
    }

    stage('built-docker-img') {
      steps {
        sh '''docker build -t myapp .
docker tag myapp hakxcore/myapp:version1.0
docker push hakxcore/myapp:version1.0'''
      }
    }

  }
}