pipeline {
  agent any
  stages {
    stage('pull-repo') {
      steps {
        git(url: 'https://github.com/hakxcore/assignment', branch: 'main')
        sh 'git pull origin'
      }
    }

    stage('build-war') {
      steps {
        sh 'mvn clean install'
      }
    }

    stage('docker-build') {
      steps {
        sh 'docker build -t myapp .'
        echo 'Docker build sucessfull'
        sh 'docker tag myapp hakxcore/myapp:version1.0'
        echo 'Image tagged with myapp:version1.0'
        sh 'docker push hakxcore/myapp:version1.0'
        echo 'Image pushed to docker hub'
      }
    }

    stage('docker-push') {
      steps {
        withDockerRegistry(hakxcore: 'docker-hub-credentials') {
          sh 'docker push hakxcore/myapp:version1.0'
        }

        echo 'Image pushed to docker hub'
      }
    }

    stage('deploy-app') {
      steps {
        echo 'Deploying Image \'myapp\''
        sh 'docker pull hakxcore/myapp:version1.0'
        echo 'Starting container'
        sh 'docker run -dit --rm -p 8888:8080 hakxcore/myapp:version1.0'
        echo 'App deployed How is \'http://ec2-52-66-190-107.ap-south-1.compute.amazonaws.com:8888/\''
      }
    }

  }
}