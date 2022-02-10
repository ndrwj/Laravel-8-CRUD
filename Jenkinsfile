pipeline {
    agent any
    stages {

        stage('Checkout Source') {
            steps {
                git url:'https://github.com/ndrwj/Laravel-8-CRUD.git', branch:'master'
            }
        }

        stage("Build") {
            environment {
                DB_HOST = credentials("laravel-mysql")
                DB_DATABASE = credentials("dblaravel")
            //    DB_USERNAME = credentials("root")
                DB_PASSWORD = credentials("password123")
            }
            steps {
                sh 'echo DB_HOST=${DB_HOST}'
                sh 'echo DB_USERNAME=${DB_USERNAME}'
                sh 'echo DB_DATABASE=${DB_DATABASE}'
                sh 'echo DB_PASSWORD=${DB_PASSWORD}'
                
            }
        }


    }
}

