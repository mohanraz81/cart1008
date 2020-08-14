pipeline {
  agent any
  stages {
    stage('mavenbuild') {
      steps {
        sh 'mvn package'
      }
    }

    stage('dockerbuild') {
      steps {
        sh '''docker build -t mohanraz81/hmsapp-frontend:1.$BUILD_NUMBER \\n docker login \\n docker push

'''
      }
    }

    stage('deploy') {
      steps {
        sh 'oc apply -f deploy/frontnend'
      }
    }

  }
}