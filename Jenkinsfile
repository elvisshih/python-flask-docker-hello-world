#!/usr/bin/env groovy
pipeline {
    agent any
    parameters {
        string(name: 'PORT', defaultValue: '5500', description: 'Forwarded Port')
    }
    stages {
        stage('Pull') {
            steps {
                git 'https://github.com/shekhargulati/python-flask-docker-hello-world.git'
            }
        }
        stage('Docker Run') {
            steps {
                sh '''docker rm -f flask-app
                docker build -t simple-flask-app:latest .
                docker run --name flask-app -d -p $PORT:5000 simple-flask-app'''
            }
        }
        stage('Smoke Test') {
            steps {
                sh 'curl 10.0.0.135:$PORT'
            }
        }
    }
}
