pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/jaehyuncho1229/GBA6270_CICD_Pipeline.git',
                branch: 'main',
                credentialsId: 'd9672def-eb08-4535-94b1-bd230a011e3b'
            }
        }
        stage('Build') {
            steps {
                sh 'chmod +x JC_build.sh'
                sh './JC_build.sh'
            }
        }
        stage('Test') {
            steps {
                sh 'chmod +x JC_test.sh'
                sh './JC_test.sh'
            }
        }
    }
    post {
        success {
            sh """
            curl -X POST https://webexapis.com/v1/messages \
            -H "Authorization: Bearer ODFmNWUyOTktM2JhMi00MTZiLWJhOTgtNjVmY2JjNzQ5YzZhZThiZTYyYmUtN2Zk_P0A1_13494cac-24b4-4f89-8247-193cc92a7636" \
            -H "Content-Type: application/json" \
            -d '{"roomId":"Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL1JPT00vMzY4YTU5NjAtODNkMy0xMWYwLTk1MzctOGZmZjRiMzVlMTEw","text":"Build #${BUILD_NUMBER} Success!"}'
            """
        }
        failure {
            sh """
            curl -X POST https://webexapis.com/v1/messages \
            -H "Authorization: Bearer ODFmNWUyOTktM2JhMi00MTZiLWJhOTgtNjVmY2JjNzQ5YzZhZThiZTYyYmUtN2Zk_P0A1_13494cac-24b4-4f89-8247-193cc92a7636" \
            -H "Content-Type: application/json" \
            -d '{"roomId":"Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL1JPT00vMzY4YTU5NjAtODNkMy0xMWYwLTk1MzctOGZmZjRiMzVlMTEw","text":"Build #${BUILD_NUMBER} Failed!"}'
            """
        }
    }
} 


