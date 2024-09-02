pipeline {
2    agent any
3    environment {
4        GITHUB_TOKEN = credentials('github-token')
5    }
6    stages {
7        stage('Checkout') {
8            steps {
9                git url: 'https://github.com/yourusername/yourrepository.git', credentialsId: 'github-credentials'
10            }
11        }
12        stage('Build') {
13            steps {
14                sh 'mvn clean install'
15            }
16        }
17        stage('Test') {
18            steps {
19                sh 'mvn test'
20            }
21        }
22        stage('Publish Test Results') {
23            steps {
24                publishHTML target: [
25                    allowMissing: false,
26                    alwaysLinkToLastBuild: true,
27                    keepAll: true,
28                    reportDir: 'target/site',
29                    reportFiles: 'index.html',
30                    reportName: 'Test Results'
31                ]
32            }
33        }
34    }
35    post {
36        success {
37            echo 'Build successful!'
38        }
39        failure {
40            echo 'Build failed!'
41        }
42    }
43}
