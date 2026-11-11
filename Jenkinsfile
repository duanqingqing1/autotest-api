pipeline {
    agent any

    stages {
        stage('执行 Newman 回归') {
            steps {
                bat '''
                    set "PATH=D:\\app_path\\nodejs;D:\\app_path\\npm-global;%PATH%"
                    if exist allure-results rmdir /s /q allure-results
                    if exist junit-result.xml del /q junit-result.xml
                    call newman run login.postman_collection.json -e local.postman_environment.json --reporters cli,junit,allure --reporter-junit-export junit-result.xml --reporter-allure-export allure-results
                '''
            }
        }
    }

    post {
        always {
            junit allowEmptyResults: true, testResults: 'junit-result.xml'
            allure includeProperties: false, jdk: '', results: [[path: 'allure-results']]
        }
    }
}
