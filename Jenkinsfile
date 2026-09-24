pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Test stage'
                sh '''
                    # build 폴더 안에 index.html 파일이 있는지 확인 
                    # (파일이 없으면 이 명령어가 실패하여 젠킨스가 자동으로 빌드를 중단)
                    test -f build/index.html
                    
                    # Node 프로젝트의 테스트 실행
                    npm test
                '''
            }
        }
    }
}