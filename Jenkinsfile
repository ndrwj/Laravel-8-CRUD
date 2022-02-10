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
                sh 'php --version'
                sh 'composer install --ignore-platform-reqs'
                sh 'composer --version'
                sh 'cp .env.example .env'
                sh 'echo DB_HOST=${DB_HOST} >> .env'
                sh 'echo DB_USERNAME=${DB_USERNAME} >> .env'
                sh 'echo DB_DATABASE=${DB_DATABASE} >> .env'
                sh 'echo DB_PASSWORD=${DB_PASSWORD} >> .env'
                sh 'php artisan key:generate'
                sh 'cp .env .env.testing'
                sh 'php artisan migrate'
            }
        }

        stage("Unit test") {
            steps {
                sh 'php artisan test'
            }
        }

        stage("Docker build") {
            steps {
                sh "docker rmi ndrwj/laravel8-test"
                sh "docker build -t ndrwj/laravel8-test ."
            }
        }

        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', '4edef996-71d4-4e10-ab5e-29d100695044') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

        stage('Deploy App to k8s') {
            steps {
                script {
                    kubernetesDeploy(configs: "laravel.yaml", kubeconfigId: "mykubeconfig")
                }
            }
        }



    }
}

