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
                DB_HOST = "laravel-mysql"
                DB_DATABASE = "dblaravel"
                DB_USERNAME = "root"
                DB_PASSWORD = credentials("mysql-password")
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

