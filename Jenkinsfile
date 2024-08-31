pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // 使用 Maven 构建代码
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // 使用 JUnit 运行测试
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code...'
                // 使用 SonarQube 进行代码分析
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // 使用 OWASP ZAP 进行安全扫描
                sh 'zap-cli scan'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // 部署到预生产环境（例如 AWS EC2）
                sh 'deploy-scripts/deploy.sh staging'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // 在预生产环境中运行集成测试
                sh 'integration-tests/run.sh staging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // 部署到生产环境
                sh 'deploy-scripts/deploy.sh production'
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed'
        }
    }
}
