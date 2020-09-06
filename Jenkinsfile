pipeline {
  agent any
  environment {
    FRONTEND_GIT = 'https://github.com/nguyenthu79/rosyCICD.git'
    FRONTEND_BRANCH = 'master'
    FRONTEND_SERVER = '1.2.3.4'
    FRONTEND_SERVER_DIR = './app'
  }
  stages {
    stage('Build JS') {
      steps {
        git(url: FRONTEND_GIT, branch: FRONTEND_BRANCH)
        sh 'clean verify allure:report -Dbrowser=Chrome -Dsuite=**/Rosy/*.story'
        stash(name: 'frontend', includes: 'build/*/**')
      }
    }

    stage('Build Image') {
      steps {
        unstash 'frontend'
        script {
          docker.withRegistry('', 'docker-hub') {
            def image = docker.build(FRONTEND_IMAGE)
            image.push(BUILD_ID)
          }
        }
      }
    }
    stage('reports') {
    steps {
    script {
            allure([
                    includeProperties: false,
                    jdk: '',
                    properties: [],
                    reportBuildPolicy: 'ALWAYS',
                    results: [[path: 'target/allure-results']]
            ])
    }
    }
}
 
}
