pipeline {
    agent any
    stages {
       stage('Build JS') {
      steps {
        git 'https://github.com/nguyenthu79/rosyCICD.git'
        sh 'clean verify allure:report -Dbrowser=Chrome -Dsuite=**/Rosy/*.story'
      
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
}
