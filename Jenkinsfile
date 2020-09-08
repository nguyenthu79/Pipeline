node {
  stage('Test') {
        git 'https://github.com/nguyenthu79/rosyCICD.git'
      
  }
  stage('Build report'){
    allure includeProperties: false, jdk: '', results: [[path: 'target\allure-results']]
  }
  stage('Send Summary'){
    emailext body: '''${SCRIPT, template="allure-report.groovy"}''',
            subject: "[Jenkins] Test Execution Summary",
            to: "thung26897@gmail.com"
  }
}
