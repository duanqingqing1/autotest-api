pipeline {
    agent any
    stages {
        stage('检出代码') {
            steps {
                checkout scm
                bat "dir"
            }
        }
        stage('执行Newman测试') {
            steps {
                bat """
newman run 底座登录+访问.postman_collection.json -e local.postman_environment.json --reporters allure --reporter-allure-export allure-results
                """
            }
        }
        stage('生成Allure报告') {
            steps {
                allure includeResults: true, results: [[path: 'allure-results']]
            }
        }
    }
}
