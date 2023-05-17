/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('build jar') {
            steps {
                script {
                    echo 'this is building block'
                    sh 'mvn package'
                }
            }
        }
        stage('build docker image') {
            steps {
                script {
                    echo 'building image'
                    /* groovylint-disable-next-line LineLength */
                    withCredentials([usernamePassword(credentialsId: 'dockerhub_credentials', passwordVariable: 'PASS', usernameVariable: 'USER')])
                        sh  'docker build -t paccciii/demo-app:jma-3.0 .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push  paccciii/demo-app:jma-3.0'
                }
            }
        }
    }
}
