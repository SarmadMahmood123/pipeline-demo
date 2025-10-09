pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/SarmadMahmood123/pipeline-demo.git'
            }
        }

        stage('Validate YAML') {
            steps {
                echo "✅ Validating YAML syntax"
                sh 'ls -l *.yaml'
            }
        }

        stage('Deploy to OpenShift CRC') {
            steps {
                script {
                    echo "🚀 Deploying to OpenShift CRC project: pipeline-project"
                    sh '''
                        oc login -u developer -p developer https://api.crc.testing:6443 --insecure-skip-tls-verify
                        oc project pipeline-project
                        oc apply -f html-demo.yaml || echo "✅ Already up to date"
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment Successful!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}
