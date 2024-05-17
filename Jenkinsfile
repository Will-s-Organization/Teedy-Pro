pipeline {
    agent any
    stages {
        stage('Install Multi-Module Project') {
            steps {
                bat 'mvn -B clean install -DskipTests'
            }
        }
        stage('PMD') {
            steps {
                bat 'mvn pmd:pmd'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Javadoc'){
            steps{
                bat 'mvn javadoc:jar'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true

    
            //  // 归档所有 Javadoc 文件
            // archiveArtifacts artifacts: '**/target/site/apidocs/**', fingerprint: true
            
            // // 归档 PMD 报告
            // archiveArtifacts artifacts: '**/target/site/pmd.html', fingerprint: true

            // // 归档所有 JAR 和 WAR 文件
            // archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            // archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true

            // 仅在构建成功时归档测试报告
            archiveArtifacts artifacts: '**/target/surefire-reports/*.xml', onlyIfSuccessful: true
        }
    }
}
