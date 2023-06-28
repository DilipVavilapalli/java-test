pipeline {
    agent any

    environment {
        function_name = 'java-sample'
    }
triggers{
        cron('*/0.10 * * * *')
    }
    stages {
        stage('Build1') {
            steps {
                echo 'Build1'
                sh 'mvn package'
            }
        }

        stage('Push') {
            steps {
                echo 'Push'

                sh "aws s3 cp target/sample-1.0.3.jar s3://bermtecbatch1996"
            }
        }

        stage('Deploy') {
            steps {
                echo 'Build1'

                sh "aws lambda update-function-code --function-name $function_name --region us-east-1 --s3-bucket bermtecbatch1996 --s3-key sample-1.0.3.jar"
            }
        }
    }
}
